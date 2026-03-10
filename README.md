# 🤖 Awesome GitHub Copilot — Power Platform & Documentation Edition

A focused collection of custom agents, instructions, and skills for GitHub Copilot — purpose-built for **Microsoft Power Platform**, **Dynamics 365**, **Dataverse**, **Power Automate**, **Power BI**, technical documentation authoring, and **C#/.NET** work in those domains.

> **Scope statement:** This repository is intentionally opinionated. Content that does not serve Power Platform, Dynamics 365, Dataverse, Power BI, Power Automate, technical documentation, or relevant C#/.NET development is out of scope and has been removed to keep the collection maintainable and signal-rich.
>
> **C# resources are intentionally preserved.** Agents, skills, instructions, and plugins that support C# work related to Dataverse, Dynamics 365 plugins, custom workflow activities, PCF component development, SDK usage, .NET automation, ASP.NET integrations, and technical documentation are all considered in scope and have been kept.

## 📦 What's Included

| Resource type | Count | Focus areas |
| --- | --- | --- |
| **👉 [Agents](docs/README.agents.md)** | 23 | Power BI, Power Platform, PCF, Dataverse, C#/.NET, docs |
| **👉 [Instructions](docs/README.instructions.md)** | ~60 | PCF (17), Dataverse Python (14), Power BI (6), Power Apps, Power Platform, C#/.NET, SQL, docs |
| **👉 [Skills](docs/README.skills.md)** | 37 | C# testing, Dataverse, Power BI, Power Platform, .NET, SQL, documentation |
| **👉 [Plugins](docs/README.plugins.md)** | 10 | Power BI, PCF, Power Apps, Power Platform, C#/.NET, Dataverse, M365 |
| **👉 [Hooks](docs/README.hooks.md)** | 3 | Session logging, auto-commit, governance |
| **👉 [Agentic Workflows](docs/README.workflows.md)** | 7 | Repo automation, relevance checks, reporting |

## 🎯 Target Scope

This repository provides GitHub Copilot customizations for:

- **Power Platform** — Power Apps (canvas, model-driven, code apps), Power Automate, Copilot Studio, connectors, ALM
- **Dynamics 365** — D365 CE, plugins, custom workflow activities, SDK integrations
- **Dataverse** — data modeling, security, Python SDK, MCP integration
- **Power BI** — DAX, data modeling, report design, performance, security/RLS, DevOps/ALM
- **Power Apps Component Framework (PCF)** — code components, Fluent UI, React, model-driven & canvas integration
- **Technical documentation** — docs authoring, Microsoft Learn contribution, markdown best practices
- **C#/.NET** — when relevant to the above areas: Dataverse plugins, D365 SDK, ASP.NET integrations, MCP server development, testing, NuGet management

## 🌟 Featured Plugins

| Name | Description | Items | Tags |
| ---- | ----------- | ----- | ---- |
| [Power BI Development](plugins/power-bi-development/README.md) | Comprehensive Power BI development resources including data modeling, DAX optimization, performance tuning, visualization design, security best practices, and DevOps/ALM guidance. | 5 items | power-bi, dax, data-modeling, performance |
| [PCF Development](plugins/pcf-development/README.md) | Complete toolkit for developing custom code components using Power Apps Component Framework for model-driven and canvas apps. | — items | power-apps, pcf, component-framework |
| [C# .NET Development](plugins/csharp-dotnet-development/README.md) | Essential prompts, instructions, and chat modes for C# and .NET development including testing, documentation, and best practices. | 9 items | csharp, dotnet, aspnet, testing |
| [Dataverse SDK for Python](plugins/dataverse-sdk-for-python/README.md) | Comprehensive collection for building production-ready Python integrations with Microsoft Dataverse. | 4 items | dataverse, python, integration, sdk |
| [Power Platform MCP Connector](plugins/power-platform-mcp-connector-development/README.md) | Complete toolkit for developing Power Platform custom connectors with MCP integration for Microsoft Copilot Studio. | 3 items | power-platform, mcp, copilot-studio |

## How to Install Customizations

To make it easy to add these customizations to your editor, we have created an [MCP Server](https://developer.microsoft.com/blog/announcing-awesome-copilot-mcp-server) that provides functionality for searching and installing instructions, agents, and skills directly from this repository. You'll need to have Docker installed and running to run the MCP server locally.

[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install-0098FF?logo=visualstudiocode&logoColor=white)](https://aka.ms/awesome-copilot/mcp/vscode) [![Install in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Install-24bfa5?logo=visualstudiocode&logoColor=white)](https://aka.ms/awesome-copilot/mcp/vscode-insiders) [![Install in Visual Studio](https://img.shields.io/badge/Visual_Studio-Install-C16FDE?logo=visualstudio&logoColor=white)](https://aka.ms/awesome-copilot/mcp/vs)

<details>
<summary>Show MCP Server JSON configuration</summary>

```json
{
  "servers": {
    "awesome-copilot": {
      "type": "stdio",
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "ghcr.io/microsoft/mcp-dotnet-samples/awesome-copilot:latest"
      ]
    }
  }
}
```

</details>

## 🔧 How to Use

### 🔌 Plugins

Plugins are installable packages that bundle related agents and skills, making it easy to install a curated set of resources.

#### Installing Plugins

First, add the Awesome Copilot marketplace to your Copilot CLI:

```bash
copilot plugin marketplace add raythekool/awesome-copilot
```

Then install any plugin:

```bash
copilot plugin install <plugin-name>@awesome-copilot
```

Alternatively, you can use the `/plugin` command within a Copilot chat session to browse and install plugins interactively.

### 🤖 Custom Agents

Custom agents can be used in Copilot coding agent (CCA), VS Code, and Copilot CLI. For CCA, when assigning an issue to Copilot, select the custom agent from the provided list. In VS Code, you can activate the custom agent in the agents session.

**Power Platform agents:** `power-platform-expert`, `power-bi-dax-expert`, `power-bi-data-modeling-expert`, `power-bi-performance-expert`, `power-bi-visualization-expert`, `power-platform-mcp-integration-expert`, `azure-logic-apps-expert`

**C#/.NET agents:** `CSharpExpert`, `expert-dotnet-software-engineer`, `csharp-dotnet-janitor`, `csharp-mcp-expert`, `microsoft-agent-framework-dotnet`, `semantic-kernel-dotnet`, `dotnet-upgrade`

**Documentation agents:** `se-technical-writer`, `gem-documentation-writer`, `microsoft_learn_contributor`, `technical-content-evaluator`, `markdown-accessibility-assistant`, `microsoft-study-mode`

**Infrastructure agents:** `ms-sql-dba`, `kusto-assistant`, `mcp-m365-agent-expert`

### 🎯 Skills

Skills are self-contained folders with instructions and bundled resources. Key skills in this collection:

- **C# testing:** `csharp-xunit`, `csharp-nunit`, `csharp-mstest`, `csharp-tunit`, `csharp-async`, `csharp-docs`
- **Dataverse:** `dataverse-python-quickstart`, `dataverse-python-production-code`, `dataverse-python-advanced-patterns`, `mcp-configure`
- **Power BI:** `power-bi-dax-optimization`, `power-bi-model-design-review`, `power-bi-performance-troubleshooting`, `power-bi-report-design-consultation`, `powerbi-modeling`
- **Power Platform:** `power-apps-code-app-scaffold`, `power-platform-mcp-connector-suite`, `flowstudio-power-automate-mcp`
- **.NET:** `dotnet-best-practices`, `dotnet-upgrade`, `nuget-manager`, `aspnet-minimal-api-openapi`
- **Documentation:** `documentation-writer`, `microsoft-docs`, `mkdocs-translations`, `create-oo-component-documentation`

### 📋 Instructions

Instructions automatically apply to files based on their patterns and provide contextual guidance for coding standards, frameworks, and best practices.

**PCF development** (17 instruction files): `pcf-overview`, `pcf-code-components`, `pcf-best-practices`, `pcf-api-reference`, `pcf-manifest-schema`, `pcf-tooling`, and more

**Dataverse Python** (14 instruction files): `dataverse-python`, `dataverse-python-best-practices`, `dataverse-python-sdk`, `dataverse-python-authentication-security`, and more

**Power BI** (6 instruction files): `power-bi-dax-best-practices`, `power-bi-data-modeling-best-practices`, `power-bi-report-design-best-practices`, and more

**C#/.NET:** `csharp`, `dotnet-architecture-good-practices`, `dotnet-framework`, `dotnet-upgrade`, `aspnet-rest-apis`, `blazor`, `copilot-sdk-csharp`, `ms-sql-dba`, `powershell`

### 🪝 Hooks

Hooks enable automated workflows triggered by specific events during GitHub Copilot coding agent sessions.

### ⚡ Agentic Workflows

Agentic Workflows are AI-powered automations that run in GitHub Actions with natural language instructions. This collection includes general-purpose repository automation workflows (daily reports, relevance checks, OSPO governance).

## 🏗️ Repository Structure

```
.
├── agents/          # 23 focused agents (Power Platform, Power BI, C#/.NET, docs)
├── instructions/    # ~60 instruction files (PCF, Dataverse, Power BI, C#/.NET, docs)
├── skills/          # 37 skills organized by domain
├── plugins/         # 10 curated plugins for Power Platform and C#/.NET
├── hooks/           # 3 automation hooks
├── workflows/       # 7 agentic workflow definitions
├── docs/            # Auto-generated README files for each resource type
└── eng/             # Build scripts (README generation, validation, marketplace)
```

## 🛠️ Development

```bash
# Install dependencies
npm ci

# Build (regenerate README.md and marketplace.json)
npm run build

# Validate plugins
npm run plugin:validate

# Validate skills
npm run skill:validate

# Fix line endings before committing
bash scripts/fix-line-endings.sh
```

## 📝 Contributing

Contributions are welcome if they are **in scope**: Power Platform, Dynamics 365, Dataverse, Power Automate, Power BI, technical documentation, or C#/.NET work for those areas.

Out-of-scope contributions (other frameworks, languages, platforms, or generic tools) will not be accepted to keep this collection maintainable and opinionated.

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines and [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) for community standards.

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.


