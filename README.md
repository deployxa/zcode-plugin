# Deployxa Plugin for ZCode (`deployxa_zcode`)

An agentic plugin enabling **ZCode** agents to autonomously trigger deployments, inspect build logs in real-time, diagnose failures, and manage project configurations on the **Deployxa** platform.

---

## Does this plugin use MCP?

**Yes, absolutely.** The plugin uses Deployxa's SDK-backed **Model Context Protocol (MCP)** server as its underlying execution and context engine. 

* **Tools**: The MCP server exposes Deployxa's API tools directly to ZCode's GLM agent (`deployxa_create_deployment`, `deployxa_get_deployment_logs`, `deployxa_diagnose_deployment`, etc.).
* **Resources**: Exposes live context via `deployxa://projects/{projectId}` and `deployxa://deployments/{deploymentId}`.
* **Skills & Commands**: The plugin packages high-level autonomous skills (`SKILL.md`) and slash commands (`/deploy`, `/diagnose`, `/logs`, `/rollback`) that direct the agent on how to coordinate MCP tools.

---

## Directory Structure

```text
├── plugin.json               # Plugin manifest (metadata & hooks)
├── .mcp.json                 # MCP server definitions
├── package.json              # Plugin package configuration
├── README.md                 # Setup & usage guide
├── commands/                 # Slash command workflows
│   ├── deploy.md             # /deploy
│   ├── diagnose.md           # /diagnose
│   ├── logs.md               # /logs
│   └── rollback.md           # /rollback
└── skills/                   # Domain skill instructions for agent
    ├── deployxa-deployment/
    │   └── SKILL.md          # Deployment lifecycle orchestration
    ├── deployxa-diagnose/
    │   └── SKILL.md          # Failure diagnostics & rollbacks
    └── deployxa-environment/
        └── SKILL.md          # Environment & domain management
```

---

## Setup & Configuration

### Prerequisites
Make sure your Deployxa token and organization ID are set:

```bash
export DEPLOYXA_TOKEN="dxa_your_api_token"
# Optional: only needed if overriding your default organization
# export DEPLOYXA_ORGANIZATION_ID="org_your_org_id"
```

### Installation in ZCode

1. **Add via ZCode Plugin Manager**:
   ```bash
   zcode plugin add github.com/deployxa/zcode-plugin
   ```

2. **Or configure `.mcp.json` in your repository root**:
   ```json
   {
     "mcpServers": {
       "deployxa": {
         "url": "https://mcp.deployxa.com/mcp"
       }
     }
   }
   ```

---

## Available Slash Commands

| Command | Description | Example |
|---|---|---|
| `/deploy [project-id] [branch]` | Trigger a new deployment and track progress | `/deploy p1 main` |
| `/diagnose [deployment-id]` | Diagnose a failed deployment using Engine evidence | `/diagnose d_123` |
| `/logs [deployment-id]` | Display bounded logs for a deployment | `/logs d_123` |
| `/rollback [deployment-id]` | Roll back to a previous healthy deployment | `/rollback d_123` |

---

## Agent Capabilities

When using natural language in ZCode:
* *"Deploy this project to Deployxa"* &rarr; Agent verifies project readiness, triggers deployment, and monitors build output.
* *"Why did my build fail?"* &rarr; Agent calls diagnostic tools to query Engine root-cause analysis and outputs fixes.
* *"Add domain api.example.com to project `my-app`"* &rarr; Agent adds domain and provides DNS record setup instructions.
