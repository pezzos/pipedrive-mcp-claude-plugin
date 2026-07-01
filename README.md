# Pipedrive MCP Claude Plugin

Private Claude plugin package for Pipedrive CRM workflows.

This repository contains two delivery pieces:

- Claude Cowork skills in `skills/`.
- The Pipedrive MCP Desktop Extension package, published as
  `pipedrive-mcp-0.1.4.mcpb`.

## Install

1. Install this repository as a private Claude plugin or marketplace source.
2. Install `pipedrive-mcp-0.1.4.mcpb` in Claude Desktop.
3. Open the Pipedrive MCP extension settings.
4. Enter the Pipedrive company domain, for example `acme` for
   `https://acme.pipedrive.com`.
5. Enter either a Pipedrive API token or an OAuth access token.
6. Enable write, Mailbox, or delete tools only when the operator needs them.
7. Save settings, then restart Claude Desktop or start a new Cowork task.

The `.mcpb` extension is the credential entry point. After credentials are
saved, it writes a managed `mcpServers.pipedrive` entry to Claude Desktop config
so Cowork can discover the local `pipedrive_*` tools. Users should not edit
`.env` files or JSON config manually.

## Safety Defaults

- Read-only CRM tools are available by default.
- Write tools require the extension setting `Enable write tools`.
- Mailbox tools require write tools and `Enable Mailbox tools`.
- Delete tools require write tools and `Enable delete tools`.
- Write calls default to dry-run unless the tool call explicitly sets
  `dry_run=false`.
- Skills instruct Claude to use only `pipedrive_*` tools, not the official
  Pipedrive connector.

## Troubleshooting

If Cowork does not see Pipedrive tools:

- Confirm the Claude plugin is installed and enabled.
- Confirm the `.mcpb` extension is installed, enabled, and configured with a
  company domain plus API/OAuth token.
- Restart Claude Desktop or start a new Cowork task after saving settings.
- Confirm Claude Desktop config contains a managed `mcpServers.pipedrive`
  entry.

The managed Desktop MCP entry contains the token as local environment
configuration for Claude Desktop. Treat Claude Desktop configuration and
extension storage as sensitive files, and rotate the Pipedrive token during
offboarding.

See `docs/CLAUDE_COWORK_PLUGIN.md` for the operator runbook.
