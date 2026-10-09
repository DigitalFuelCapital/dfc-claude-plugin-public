# EcommIQ

Ask your assistant questions about your company's ecommerce data in plain language: revenue, orders, AOV,
customers, retention, marketing spend and ROAS. The plugin connects Claude or Codex to
[EcommIQ](https://ecommiq.tools), the business intelligence platform owned and operated by
[Digital Fuel Capital](https://digitalfuelcapital.com) (DFC).

## Requirements

You need an EcommIQ account at [ecommiq.tools](https://ecommiq.tools), and Digital Fuel Capital must
have turned on AI access for your company. You only see data for the companies your account can
access.

## What the plugin contains

- **`ecommiq` MCP server.** A remote server at `https://ecommiq.tools/api/mcp/v1/ecommiq`. You sign
  in with OAuth at ecommiq.tools. Your AI client never sees your password.
- **`report-navigator` skill.** Teaches the assistant to find which EcommIQ report answers a question,
  where it sits in the sidebar, and which metrics and filters it supports.

The plugin has no hooks, commands, local scripts or package installs.

## Installation and compatibility

Follow the [repository installation guide](https://github.com/DigitalFuelCapital/dfc-claude-plugin-public/blob/main/README.md)
for Claude and Codex.
Codex uses the portable `plugin.json` and `mcp.json`; Claude uses `.claude-plugin/plugin.json`
and `.mcp.json`. Both clients load the same `skills/` directory and connect to the same server.
Sign in separately in each client. Server-side OAuth support and your account's AI access are
required; the package does not grant additional permissions.

Other clients can use the MCP endpoint if they support Streamable HTTP and the server's OAuth
flow. A direct MCP connection does not automatically install the bundled skill.

## What the connector can do

- List the companies and data sources your account can access.
- Find and explain EcommIQ reports.
- Answer questions using governed business metrics, so figures match their EcommIQ definitions.
- Run read-only SQL queries against your company's data, including longer queries in the
  background.
- Report a problem to the EcommIQ team.

The plugin is read-only for your business data: it cannot change or delete it.

## Data handling

The plugin talks only to `ecommiq.tools`. Report descriptions and query results are returned to
your AI client as part of your conversation. EcommIQ records each tool request (user, tool, parameters,
result summary and timing) for security, auditing and support, and may cache query results for up
to 24 hours. Issue reports you ask the assistant to file are sent to the EcommIQ team. Access is checked on
every request and stops immediately if your account or your company's AI access is turned off. See
the [EcommIQ privacy policy](https://ecommiq.tools/policy/privacy).

## Support

Ask your assistant to "report an issue with EcommIQ", or contact your Digital Fuel Capital team or
[policy@ecommiq.tools](mailto:policy@ecommiq.tools).

## License

[MIT](https://github.com/DigitalFuelCapital/dfc-claude-plugin-public/blob/main/LICENSE)
