# Pipedrive MCP

This repository publishes the Pipedrive MCP delivery bundle for Claude.

It contains two separate pieces:

- `pipedrive-mcp-0.1.3.mcpb`: Claude Desktop Extension that installs the local
  MCP connector and exposes editable settings for Pipedrive credentials.
- `Pipedrive MCP` marketplace plugin: Claude Cowork skills that route natural
  language CRM requests to `pipedrive_*` tools.

Use both pieces together. The repository plugin is skills-only on purpose. It
does not define its own connector because the Cowork plugin Connectors tab is a
read-only view and is not the right place for API-key entry.

## Install The Connector

Install `pipedrive-mcp-0.1.3.mcpb` in Claude Desktop:

1. Open Claude Desktop settings.
2. Go to Extensions.
3. Open Advanced settings.
4. Click Install Extension.
5. Select `pipedrive-mcp-0.1.3.mcpb`.
6. Fill the extension settings:
   - Pipedrive company domain: enter only the company subdomain, not the full
     URL.
   - Pipedrive API token, or OAuth access token where required.
   - Optional write, Mailbox, delete, and timeout settings.

Do not paste API keys into a Claude conversation and do not rely on a local
`.env` file for client delivery.

## Install The Cowork Skills

After the Desktop Extension is installed and configured, add this repository as
a personal Claude plugin marketplace:

```text
pezzos/pipedrive-mcp-claude-plugin
```

Install `Pipedrive MCP` from the Personal tab. This provides the Cowork skills
only. The actual connector is the Desktop Extension installed from the `.mcpb`.

## Smoke Test

Start a new Claude/Cowork session and ask:

```text
Use Pipedrive MCP only. Run the pipedrive_health_check tool and report whether
Pipedrive MCP is connected. Do not use the official Pipedrive connector.
```

Expected result after settings are filled:

- `token_configured: true`
- `company_domain_configured: true`
- `writes_enabled: false` unless explicitly enabled

If Claude says no `pipedrive_*` tools are available, restart Claude Desktop and
start a new Cowork session.

## Contents

- `.claude-plugin/marketplace.json`: private marketplace manifest.
- `.claude-plugin/plugin.json`: skills-only Cowork plugin manifest.
- `skills/`: Pipedrive workflow skills.
- `mcpb/pipedrive-mcp/`: unpacked Desktop Extension source.
- `pipedrive-mcp-0.1.3.mcpb`: installable Desktop Extension.
