---
description: 'Best practices and patterns for developing Dataverse plugins and custom workflow activities using C# and the Dataverse SDK for .NET'
applyTo: '**/*.{cs,csproj,sln}'
---

# Dataverse C# Plugin Development

This instruction file provides guidance for developing Dataverse plugins, custom workflow activities, and SDK-based integrations using C# and the Microsoft Dataverse SDK for .NET.

## Project Setup

### NuGet Packages

For Dataverse plugin projects, use the following packages:

```xml
<PackageReference Include="Microsoft.CrmSdk.CoreAssemblies" Version="9.0.2.*" />
<!-- Or for Dataverse-only (no legacy CRM) -->
<PackageReference Include="Microsoft.PowerPlatform.Dataverse.Client" Version="1.*" />
```

For early-bound entity generation:

```bash
pac modelbuilder build --namespace YourNamespace --outputDirectory ./Model
```

### Plugin Project Structure

```
MyPlugin/
├── MyPlugin.csproj
├── Plugins/
│   └── AccountCreatedPlugin.cs
├── WorkflowActivities/
│   └── SendNotificationActivity.cs
├── Model/          # Early-bound entities (generated)
└── spkl.json       # spkl deployment configuration
```

## Plugin Development Patterns

### Basic Plugin Structure

```csharp
using Microsoft.Xrm.Sdk;
using System;
using System.ServiceModel;

namespace MyOrg.Plugins
{
    /// <summary>
    /// Plugin that executes on account creation to set default values.
    /// Register: Account, Create, PostOperation, Synchronous
    /// </summary>
    public class AccountCreatedPlugin : IPlugin
    {
        public void Execute(IServiceProvider serviceProvider)
        {
            // Get required services from the service provider
            var tracingService = (ITracingService)serviceProvider.GetService(typeof(ITracingService));
            var context = (IPluginExecutionContext)serviceProvider.GetService(typeof(IPluginExecutionContext));
            var serviceFactory = (IOrganizationServiceFactory)serviceProvider.GetService(typeof(IOrganizationServiceFactory));
            var service = serviceFactory.CreateOrganizationService(context.UserId);

            try
            {
                tracingService.Trace("AccountCreatedPlugin: Start. Entity={0}, Stage={1}, Mode={2}",
                    context.PrimaryEntityName, context.Stage, context.Mode);

                // Validate the context
                if (context.InputParameters.Contains("Target") &&
                    context.InputParameters["Target"] is Entity target)
                {
                    if (target.LogicalName != "account")
                        return;

                    // Your plugin logic here
                    var accountName = target.GetAttributeValue<string>("name");
                    tracingService.Trace("Processing account: {0}", accountName ?? "(null)");

                    // Example: update the entity after creation
                    var update = new Entity("account", target.Id)
                    {
                        ["description"] = $"Created via plugin at {DateTime.UtcNow:o}"
                    };
                    service.Update(update);
                }
            }
            catch (InvalidPluginExecutionException)
            {
                throw; // Re-throw plugin validation exceptions as-is
            }
            catch (FaultException<OrganizationServiceFault> ex)
            {
                tracingService.Trace("Organization service fault: {0}", ex.Detail?.Message);
                throw new InvalidPluginExecutionException(
                    $"An error occurred in AccountCreatedPlugin: {ex.Detail?.Message}", ex);
            }
            catch (Exception ex)
            {
                tracingService.Trace("Unexpected error: {0}", ex);
                throw new InvalidPluginExecutionException(
                    $"Unexpected error in AccountCreatedPlugin: {ex.Message}", ex);
            }
        }
    }
}
```

### Pre-Image and Post-Image Usage

```csharp
// PreImage: state of the entity BEFORE the operation (register with name "PreImage")
if (context.PreEntityImages.Contains("PreImage"))
{
    var preImage = context.PreEntityImages["PreImage"];
    var previousName = preImage.GetAttributeValue<string>("name");
}

// PostImage: state of the entity AFTER the operation (register with name "PostImage")
if (context.PostEntityImages.Contains("PostImage"))
{
    var postImage = context.PostEntityImages["PostImage"];
    var newName = postImage.GetAttributeValue<string>("name");
}
```

### Shared Variables and Depth Check

```csharp
// Prevent infinite loops in recursive plugin scenarios
if (context.Depth > 1)
    return;

// Share data between plugins in the same execution pipeline
if (!context.SharedVariables.Contains("ProcessedByMyPlugin"))
{
    context.SharedVariables["ProcessedByMyPlugin"] = true;
    // ... process ...
}
```

## Custom Workflow Activities

```csharp
using Microsoft.Xrm.Sdk;
using Microsoft.Xrm.Sdk.Workflow;
using System.Activities;

namespace MyOrg.WorkflowActivities
{
    public class SendNotificationActivity : CodeActivity
    {
        [RequiredArgument]
        [Input("Account Name")]
        public InArgument<string> AccountName { get; set; }

        [Output("Notification Status")]
        public OutArgument<string> NotificationStatus { get; set; }

        protected override void Execute(CodeActivityContext context)
        {
            var workflowContext = context.GetExtension<IWorkflowContext>();
            var serviceFactory = context.GetExtension<IOrganizationServiceFactory>();
            var service = serviceFactory.CreateOrganizationService(workflowContext.UserId);
            var tracingService = context.GetExtension<ITracingService>();

            var accountName = AccountName.Get(context);
            tracingService.Trace("SendNotificationActivity: AccountName={0}", accountName);

            // Your workflow activity logic here
            NotificationStatus.Set(context, "Sent");
        }
    }
}
```

## Querying Dataverse

### QueryExpression (recommended for typed queries)

```csharp
var query = new QueryExpression("contact")
{
    ColumnSet = new ColumnSet("fullname", "emailaddress1", "accountid"),
    Criteria = new FilterExpression
    {
        Conditions =
        {
            new ConditionExpression("statecode", ConditionOperator.Equal, 0), // Active
            new ConditionExpression("emailaddress1", ConditionOperator.NotNull)
        }
    },
    Orders = { new OrderExpression("fullname", OrderType.Ascending) },
    TopCount = 50
};

var results = service.RetrieveMultiple(query);
```

### FetchXML (recommended for complex queries and aggregation)

```csharp
string fetchXml = @"
<fetch aggregate='true'>
  <entity name='opportunity'>
    <attribute name='estimatedvalue' aggregate='sum' alias='total_value' />
    <attribute name='ownerid' groupby='true' alias='owner' />
    <filter>
      <condition attribute='statecode' operator='eq' value='0' />
    </filter>
  </entity>
</fetch>";

var results = service.RetrieveMultiple(new FetchExpression(fetchXml));
```

### Paging Large Result Sets

```csharp
var query = new QueryExpression("contact") { PageInfo = new PagingInfo { Count = 5000, PageNumber = 1 } };
query.ColumnSet = new ColumnSet("fullname");

EntityCollection results;
do
{
    results = service.RetrieveMultiple(query);
    foreach (var entity in results.Entities)
    {
        // process entity
    }
    query.PageInfo.PageNumber++;
    query.PageInfo.PagingCookie = results.PagingCookie;
} while (results.MoreRecords);
```

## Batch Operations

```csharp
// Use ExecuteMultipleRequest for bulk operations
var requests = new ExecuteMultipleRequest
{
    Requests = new OrganizationRequestCollection(),
    Settings = new ExecuteMultipleSettings { ContinueOnError = true, ReturnResponses = true }
};

foreach (var contactId in contactIds)
{
    requests.Requests.Add(new UpdateRequest
    {
        Target = new Entity("contact", contactId) { ["description"] = "Updated in bulk" }
    });
}

var response = (ExecuteMultipleResponse)service.Execute(requests);
```

## Best Practices

### Plugin Registration

- Use **spkl** (`dotnet tool install spkl -g`) or **PAC CLI** (`pac plugin push`) for automated plugin registration
- Always specify filtering attributes to limit plugin execution to relevant attribute changes
- Use asynchronous execution for long-running operations (emails, external calls)
- Prefer PostOperation for most business logic; use PreValidation for validation rules

### Security and Context

- Use `context.UserId` (calling user) vs `Guid.Empty` (system user) based on business needs
- Avoid hardcoded GUIDs for system records; use `RetrieveMultiple` to look up by name/code
- Store configuration in Dataverse environment variables or custom configuration entities, not in plugin code

### Performance

- Only retrieve columns you need (`ColumnSet` with specific attributes, not `new ColumnSet(true)`)
- Minimize service calls: batch related operations using `ExecuteMultipleRequest`
- Use `FilteringAttributes` to prevent the plugin from firing on unrelated updates
- For large data processing, use asynchronous plugins or Azure Functions triggered via Service Bus

### Testing with FakeXrmEasy

```csharp
// Using FakeXrmEasy for unit testing plugins
var ctx = new XrmFakedContext();
ctx.Initialize(new List<Entity>
{
    new Entity("account", Guid.NewGuid()) { ["name"] = "Test Account" }
});

var pluginContext = ctx.GetDefaultPluginContext();
pluginContext.InputParameters["Target"] = new Entity("account", Guid.NewGuid()) { ["name"] = "New Account" };
pluginContext.Stage = 40; // PostOperation
pluginContext.MessageName = "Create";

ctx.ExecutePluginWith<AccountCreatedPlugin>(pluginContext);

// Assert: verify the expected updates were made
var updatedAccount = ctx.Data["account"].Values.First();
Assert.IsNotNull(updatedAccount["description"]);
```

## Deployment Checklist

- [ ] Plugin assembly signed with strong name key
- [ ] Target .NET Framework 4.6.2 (or 4.8 for full trust) / .NET 6+ for isolated plugins
- [ ] Filtering attributes configured to minimize unnecessary plugin executions
- [ ] Plugin registered with Plugin Registration Tool or automated via spkl/PAC CLI
- [ ] Pre-images and post-images registered where needed
- [ ] Tested in developer/sandbox environment before production deployment
- [ ] Plugin included in a Dataverse solution for ALM
