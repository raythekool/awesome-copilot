# 🎯 Agent Skills

Agent Skills are self-contained folders with instructions and bundled resources that enhance AI capabilities for specialized tasks. Based on the [Agent Skills specification](https://agentskills.io/specification), each skill contains a `SKILL.md` file with detailed instructions that agents load on-demand.

Skills differ from other primitives by supporting bundled assets (scripts, code samples, reference data) that agents can utilize when performing specialized tasks.
### How to Contribute

See [CONTRIBUTING.md](../CONTRIBUTING.md#adding-skills) for guidelines on how to contribute new agent skills, improve existing ones, and share your use cases.

### How to Use Agent Skills

**What's Included:**
- Each skill is a folder containing a `SKILL.md` instruction file
- Skills may include helper scripts, code templates, or reference data
- Skills follow the Agent Skills specification for maximum compatibility

**When to Use:**
- Skills are ideal for complex, repeatable workflows that benefit from bundled resources
- Use skills when you need code templates, helper utilities, or reference data alongside instructions
- Skills provide progressive disclosure - loaded only when needed for specific tasks

**Usage:**
- Browse the skills table below to find relevant capabilities
- Copy the skill folder to your local skills directory
- Reference skills in your prompts or let the agent discover them automatically

| Name | Description | Bundled Assets |
| ---- | ----------- | -------------- |
| [aspnet-minimal-api-openapi](../skills/aspnet-minimal-api-openapi/SKILL.md) | Create ASP.NET Minimal API endpoints with proper OpenAPI documentation | None |
| [create-oo-component-documentation](../skills/create-oo-component-documentation/SKILL.md) | Create comprehensive, standardized documentation for object-oriented components following industry best practices and architectural documentation standards. | None |
| [csharp-async](../skills/csharp-async/SKILL.md) | Get best practices for C# async programming | None |
| [csharp-docs](../skills/csharp-docs/SKILL.md) | Ensure that C# types are documented with XML comments and follow best practices for documentation. | None |
| [csharp-mcp-server-generator](../skills/csharp-mcp-server-generator/SKILL.md) | Generate a complete MCP server project in C# with tools, prompts, and proper configuration | None |
| [csharp-mstest](../skills/csharp-mstest/SKILL.md) | Get best practices for MSTest 3.x/4.x unit testing, including modern assertion APIs and data-driven tests | None |
| [csharp-nunit](../skills/csharp-nunit/SKILL.md) | Get best practices for NUnit unit testing, including data-driven tests | None |
| [csharp-tunit](../skills/csharp-tunit/SKILL.md) | Get best practices for TUnit unit testing, including data-driven tests | None |
| [csharp-xunit](../skills/csharp-xunit/SKILL.md) | Get best practices for XUnit unit testing, including data-driven tests | None |
| [dataverse-python-advanced-patterns](../skills/dataverse-python-advanced-patterns/SKILL.md) | Generate production code for Dataverse SDK using advanced patterns, error handling, and optimization techniques. | None |
| [dataverse-python-production-code](../skills/dataverse-python-production-code/SKILL.md) | Generate production-ready Python code using Dataverse SDK with error handling, optimization, and best practices | None |
| [dataverse-python-quickstart](../skills/dataverse-python-quickstart/SKILL.md) | Generate Python SDK setup + CRUD + bulk + paging snippets using official patterns. | None |
| [dataverse-python-usecase-builder](../skills/dataverse-python-usecase-builder/SKILL.md) | Generate complete solutions for specific Dataverse SDK use cases with architecture recommendations | None |
| [documentation-writer](../skills/documentation-writer/SKILL.md) | Diátaxis Documentation Expert. An expert technical writer specializing in creating high-quality software documentation, guided by the principles and structure of the Diátaxis technical documentation authoring framework. | None |
| [dotnet-best-practices](../skills/dotnet-best-practices/SKILL.md) | Ensure .NET/C# code meets best practices for the solution/project. | None |
| [dotnet-design-pattern-review](../skills/dotnet-design-pattern-review/SKILL.md) | Review the C#/.NET code for design pattern implementation and suggest improvements. | None |
| [dotnet-upgrade](../skills/dotnet-upgrade/SKILL.md) | Ready-to-use prompts for comprehensive .NET framework upgrade analysis and execution | None |
| [flowstudio-power-automate-mcp](../skills/flowstudio-power-automate-mcp/SKILL.md) | Connect to and operate Power Automate cloud flows via a FlowStudio MCP server. Use when asked to: list flows, read a flow definition, check run history, inspect action outputs, resubmit a run, cancel a running flow, view connections, get a trigger URL, validate a definition, monitor flow health, or any task that requires talking to the Power Automate API through an MCP tool. Also use for Power Platform environment discovery and connection management. Requires a FlowStudio MCP subscription or compatible server — see https://mcp.flowstudio.app | `references/MCP-BOOTSTRAP.md`<br />`references/action-types.md`<br />`references/connection-references.md`<br />`references/tool-reference.md` |
| [mcp-configure](../skills/mcp-configure/SKILL.md) | Configure an MCP server for GitHub Copilot with your Dataverse environment. | None |
| [mcp-copilot-studio-server-generator](../skills/mcp-copilot-studio-server-generator/SKILL.md) | Generate a complete MCP server implementation optimized for Copilot Studio integration with proper schema constraints and streamable HTTP support | None |
| [mcp-create-adaptive-cards](../skills/mcp-create-adaptive-cards/SKILL.md) | Skill converted from mcp-create-adaptive-cards.prompt.md | None |
| [mcp-create-declarative-agent](../skills/mcp-create-declarative-agent/SKILL.md) | Skill converted from mcp-create-declarative-agent.prompt.md | None |
| [mcp-deploy-manage-agents](../skills/mcp-deploy-manage-agents/SKILL.md) | Skill converted from mcp-deploy-manage-agents.prompt.md | None |
| [microsoft-docs](../skills/microsoft-docs/SKILL.md) | Query official Microsoft documentation to find concepts, tutorials, and code examples across Azure, .NET, Agent Framework, Aspire, VS Code, GitHub, and more. Uses Microsoft Learn MCP as the default, with Context7 and Aspire MCP for content that lives outside learn.microsoft.com. | None |
| [mkdocs-translations](../skills/mkdocs-translations/SKILL.md) | Generate a language translation for a mkdocs documentation stack. | None |
| [nuget-manager](../skills/nuget-manager/SKILL.md) | Manage NuGet packages in .NET projects/solutions. Use this skill when adding, removing, or updating NuGet package versions. It enforces using `dotnet` CLI for package management and provides strict procedures for direct file edits only when updating versions. | None |
| [openapi-to-application-code](../skills/openapi-to-application-code/SKILL.md) | Generate a complete, production-ready application from an OpenAPI specification | None |
| [power-apps-code-app-scaffold](../skills/power-apps-code-app-scaffold/SKILL.md) | Scaffold a complete Power Apps Code App project with PAC CLI setup, SDK integration, and connector configuration | None |
| [power-bi-dax-optimization](../skills/power-bi-dax-optimization/SKILL.md) | Comprehensive Power BI DAX formula optimization prompt for improving performance, readability, and maintainability of DAX calculations. | None |
| [power-bi-model-design-review](../skills/power-bi-model-design-review/SKILL.md) | Comprehensive Power BI data model design review prompt for evaluating model architecture, relationships, and optimization opportunities. | None |
| [power-bi-performance-troubleshooting](../skills/power-bi-performance-troubleshooting/SKILL.md) | Systematic Power BI performance troubleshooting prompt for identifying, diagnosing, and resolving performance issues in Power BI models, reports, and queries. | None |
| [power-bi-report-design-consultation](../skills/power-bi-report-design-consultation/SKILL.md) | Power BI report visualization design prompt for creating effective, user-friendly, and accessible reports with optimal chart selection and layout design. | None |
| [power-platform-mcp-connector-suite](../skills/power-platform-mcp-connector-suite/SKILL.md) | Generate complete Power Platform custom connector with MCP integration for Copilot Studio - includes schema generation, troubleshooting, and validation | None |
| [powerbi-modeling](../skills/powerbi-modeling/SKILL.md) | Power BI semantic modeling assistant for building optimized data models. Use when working with Power BI semantic models, creating measures, designing star schemas, configuring relationships, implementing RLS, or optimizing model performance. Triggers on queries about DAX calculations, table relationships, dimension/fact table design, naming conventions, model documentation, cardinality, cross-filter direction, calculation groups, and data model best practices. Always connects to the active model first using power-bi-modeling MCP tools to understand the data structure before providing guidance. | `references/MEASURES-DAX.md`<br />`references/PERFORMANCE.md`<br />`references/RELATIONSHIPS.md`<br />`references/RLS.md`<br />`references/STAR-SCHEMA.md` |
| [sql-code-review](../skills/sql-code-review/SKILL.md) | Universal SQL code review assistant that performs comprehensive security, maintainability, and code quality analysis across all SQL databases (MySQL, PostgreSQL, SQL Server, Oracle). Focuses on SQL injection prevention, access control, code standards, and anti-pattern detection. Complements SQL optimization prompt for complete development coverage. | None |
| [sql-optimization](../skills/sql-optimization/SKILL.md) | Universal SQL performance optimization assistant for comprehensive query tuning, indexing strategies, and database performance analysis across all SQL databases (MySQL, PostgreSQL, SQL Server, Oracle). Provides execution plan analysis, pagination optimization, batch operations, and performance monitoring guidance. | None |
| [update-oo-component-documentation](../skills/update-oo-component-documentation/SKILL.md) | Update existing object-oriented component documentation following industry best practices and architectural documentation standards. | None |
