# EcommIQ connector

Install the EcommIQ plugin to connect Claude or Codex to [EcommIQ](https://ecommiq.tools) and ask questions about your company's ecommerce
data in plain language: revenue, orders, AOV, customers, retention, marketing spend and ROAS.

EcommIQ ([ecommiq.tools](https://ecommiq.tools)) is owned and operated by
[Digital Fuel Capital](https://digitalfuelcapital.com) (DFC). This
repository contains DFC's EcommIQ plugin and marketplaces for Claude and Codex. The plugin is published and maintained
by DFC. The plugin contains the connector configuration and a report-navigation skill; all data
access, sign-in and permissions are handled by EcommIQ.

## Who can use it

You need an EcommIQ account at [ecommiq.tools](https://ecommiq.tools), and Digital Fuel Capital must
have turned on AI access for your company. You only see data for the companies your account can
access. If sign-in succeeds but your AI client reports that access is denied, ask your Digital Fuel Capital
contact to enable AI access for your company.

## Install in Codex

Use a current Codex CLI with `codex plugin` support:

```sh
codex plugin marketplace add DigitalFuelCapital/dfc-claude-plugin-public
codex plugin add ecommiq@dfc
```

Restart the desktop app or start a new CLI session, and authenticate with EcommIQ when prompted.
In the CLI, use `/plugins` to inspect the installed plugin and `/mcp` to check the server connection.
The marketplace installs both the `ecommiq` MCP server and the `report-navigator` skill.

For local development, add the repository checkout instead of the GitHub source:

```sh
codex plugin marketplace add /absolute/path/to/dfc-claude-plugin-public
codex plugin add ecommiq@dfc
```

Codex and Claude authenticate separately. An existing Claude connection does not grant Codex access.
If OAuth fails, ask DFC to check the server's client-registration and callback support for Codex;
this repository packages the connector but does not implement the authentication server.

See OpenAI's [plugin packaging](https://developers.openai.com/plugins/build/plugins) and
[MCP setup](https://learn.chatgpt.com/docs/extend/mcp?surface=cli) documentation.

## Connect another MCP client

The same EcommIQ backend can be configured directly in clients that support Streamable HTTP MCP
and the server's OAuth flow:

```text
https://ecommiq.tools/api/mcp/v1/ecommiq
```

For example, to connect only the server in Codex without installing the plugin:

```sh
codex mcp add ecommiq --url https://ecommiq.tools/api/mcp/v1/ecommiq
codex mcp login ecommiq
```

This server-only setup does not install the report-navigation skill. Choose either the plugin or
the direct server setup to avoid duplicate tools. Other MCP clients need their own configuration
and authentication; their compatibility is not established by the plugin package alone.

## Install in claude.ai or Claude Desktop

Each person adds the DFC marketplace to their own account. Right now this is the only way to
install the plugin in claude.ai and Claude Desktop.

1. Open **Customize → Plugins**, choose **Add → Add marketplace**, and enter the GitHub
   URL:
   ```
   https://github.com/DigitalFuelCapital/dfc-claude-plugin-public
   ```
2. Open **Discover**, select **EcommIQ** and click **Install**.
3. Open **Customize → Plugins → EcommIQ → Connectors** and connect `ecommiq`. A browser window opens
   at ecommiq.tools: sign in if prompted, then click **Approve**.
4. Start a new chat and ask a question, for example "What was revenue by month this year?"

To get updates, use **Check for updates** on the marketplace or turn on **Sync automatically**.
Plugins added here also appear in the Claude Desktop Code tab and in Claude Code.

## Install for your whole Claude organization (Team and Enterprise)

**In progress.** Organization-wide install is not available yet. **Organization settings → Plugins &
skills** can only sync private or internal GitHub repositories, and this marketplace is public. Until
this is supported, each member should install the plugin from their own account as described above.

## Install in Claude Code

If you added the marketplace in claude.ai or Claude Desktop, the plugin already syncs to Claude Code.
To install it in Claude Code only:

```
/plugin marketplace add DigitalFuelCapital/dfc-claude-plugin-public
/plugin install ecommiq@dfc
```

The first time Claude uses an EcommIQ tool, Claude Code opens the same browser sign-in. Run `/mcp`
to check that the `ecommiq` server is connected.

To get updates later:

```
/plugin marketplace update dfc
```

## What the connector can do

- List the companies and data sources your account can access.
- Find which EcommIQ report covers a question, where it sits in the sidebar, and which metrics
  and filters it supports.
- Answer questions using governed business metrics, so figures match their EcommIQ definitions.
- Run read-only SQL queries against your company's data for ad-hoc analysis, including longer
  queries in the background.
- Report a problem with EcommIQ to the EcommIQ team.

The plugin is read-only for your business data: it cannot change or delete it. Issue reports you
ask the assistant to file are sent to the EcommIQ team.

## Package layout

- `plugins/ecommiq/plugin.json` and `mcp.json`: portable plugin metadata and MCP configuration,
  including Codex presentation metadata in `extensions.com.openai`.
- `.agents/plugins/marketplace.json`: Codex marketplace pointing to the shared plugin directory.
- `.claude-plugin/marketplace.json` and `plugins/ecommiq/.claude-plugin/plugin.json`: Claude
  marketplace and plugin metadata.
- `plugins/ecommiq/.mcp.json`: the same MCP endpoint in Claude's configuration format.
- `plugins/ecommiq/skills/`: shared client-neutral skills.

When releasing an update, keep the portable and Claude plugin identity, version and description
aligned with the Claude marketplace entry. Keep the endpoint in `mcp.json` and `.mcp.json` aligned;
their transport labels differ (`streamable-http` and `http`).

## Privacy and security

- Sign-in uses OAuth 2.1 with PKCE. The AI client never sees your EcommIQ password.
- Access is checked on every request. If your account or your company's AI access is turned off,
  the plugin stops working immediately.
- Query results are returned to your AI client as part of your conversation and are subject to
  that client's plan and workspace data retention settings.

## Support

Ask your assistant to "report an issue with EcommIQ", or contact your Digital Fuel Capital team.

## License

[MIT](LICENSE)
