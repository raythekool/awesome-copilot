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
| [csharp-docs](../skills/csharp-docs/SKILL.md) | Ensure that C# types are documented with XML comments and follow best practices for documentation. | None |
| [dataverse-python-advanced-patterns](../skills/dataverse-python-advanced-patterns/SKILL.md) | Generate production code for Dataverse SDK using advanced patterns, error handling, and optimization techniques. | None |
| [dataverse-python-production-code](../skills/dataverse-python-production-code/SKILL.md) | Generate production-ready Python code using Dataverse SDK with error handling, optimization, and best practices | None |
| [dataverse-python-quickstart](../skills/dataverse-python-quickstart/SKILL.md) | Generate Python SDK setup + CRUD + bulk + paging snippets using official patterns. | None |
| [dataverse-python-usecase-builder](../skills/dataverse-python-usecase-builder/SKILL.md) | Generate complete solutions for specific Dataverse SDK use cases with architecture recommendations | None |
| [documentation-writer](../skills/documentation-writer/SKILL.md) | Diátaxis Documentation Expert. An expert technical writer specializing in creating high-quality software documentation, guided by the principles and structure of the Diátaxis technical documentation authoring framework. | None |
| [flowstudio-power-automate-mcp](../skills/flowstudio-power-automate-mcp/SKILL.md) | Connect to and operate Power Automate cloud flows via a FlowStudio MCP server. Use when asked to: list flows, read a flow definition, check run history, inspect action outputs, resubmit a run, cancel a running flow, view connections, get a trigger URL, validate a definition, monitor flow health, or any task that requires talking to the Power Automate API through an MCP tool. Also use for Power Platform environment discovery and connection management. Requires a FlowStudio MCP subscription or compatible server — see https://mcp.flowstudio.app | `references/MCP-BOOTSTRAP.md`<br />`references/action-types.md`<br />`references/connection-references.md`<br />`references/tool-reference.md` |
| [microsoft-docs](../skills/microsoft-docs/SKILL.md) | Query official Microsoft documentation to find concepts, tutorials, and code examples across Azure, .NET, Agent Framework, Aspire, VS Code, GitHub, and more. Uses Microsoft Learn MCP as the default, with Context7 and Aspire MCP for content that lives outside learn.microsoft.com. | None |
| [power-apps-code-app-scaffold](../skills/power-apps-code-app-scaffold/SKILL.md) | Scaffold a complete Power Apps Code App project with PAC CLI setup, SDK integration, and connector configuration | None |
| [power-bi-dax-optimization](../skills/power-bi-dax-optimization/SKILL.md) | Comprehensive Power BI DAX formula optimization prompt for improving performance, readability, and maintainability of DAX calculations. | None |
| [power-bi-model-design-review](../skills/power-bi-model-design-review/SKILL.md) | Comprehensive Power BI data model design review prompt for evaluating model architecture, relationships, and optimization opportunities. | None |
| [power-bi-performance-troubleshooting](../skills/power-bi-performance-troubleshooting/SKILL.md) | Systematic Power BI performance troubleshooting prompt for identifying, diagnosing, and resolving performance issues in Power BI models, reports, and queries. | None |
| [power-bi-report-design-consultation](../skills/power-bi-report-design-consultation/SKILL.md) | Power BI report visualization design prompt for creating effective, user-friendly, and accessible reports with optimal chart selection and layout design. | None |
| [power-platform-mcp-connector-suite](../skills/power-platform-mcp-connector-suite/SKILL.md) | Generate complete Power Platform custom connector with MCP integration for Copilot Studio - includes schema generation, troubleshooting, and validation | None |
| [powerbi-modeling](../skills/powerbi-modeling/SKILL.md) | Power BI semantic modeling assistant for building optimized data models. Use when working with Power BI semantic models, creating measures, designing star schemas, configuring relationships, implementing RLS, or optimizing model performance. Triggers on queries about DAX calculations, table relationships, dimension/fact table design, naming conventions, model documentation, cardinality, cross-filter direction, calculation groups, and data model best practices. Always connects to the active model first using power-bi-modeling MCP tools to understand the data structure before providing guidance. | `references/MEASURES-DAX.md`<br />`references/PERFORMANCE.md`<br />`references/RELATIONSHIPS.md`<br />`references/RLS.md`<br />`references/STAR-SCHEMA.md` |
