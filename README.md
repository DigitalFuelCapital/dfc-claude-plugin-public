# EcommIQ for Claude

Connect Claude to [EcommIQ](https://ecommiq.tools) and ask questions about your company's ecommerce
data in plain language: revenue, orders, AOV, customers, retention, marketing spend and ROAS.

EcommIQ ([ecommiq.tools](https://ecommiq.tools)) is owned and operated by
[Digital Fuel Capital](https://digitalfuelcapital.com) (DFC). This
repository is DFC's Claude Code plugin marketplace, and the EcommIQ plugin is published and maintained
by DFC. The plugin contains the connector configuration and a report-navigation skill; all data
access, sign-in and permissions are handled by EcommIQ.

## Who can use it

You need an EcommIQ account at [ecommiq.tools](https://ecommiq.tools), and Digital Fuel Capital must
have turned on AI access for your company. You only see data for the companies your account can
access. If sign-in succeeds but Claude reports that access is denied, ask your Digital Fuel Capital
contact to enable AI access for your company.

## Connect in claude.ai or Claude Desktop

1. Open **Settings → Connectors** and choose **Add custom connector**.
2. Name it `EcommIQ` and enter the URL:
   ```
   https://ecommiq.tools/api/mcp/v1/ecommiq
   ```
3. Click **Connect**. A browser window opens at ecommiq.tools: sign in if prompted, then click
   **Approve**.
4. Start a new chat and ask a question, for example "What was revenue by month this year?"

On Team and Enterprise plans an organization owner may need to add the connector first, under
**Organization settings → Connectors**.

## Install in Claude Code

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

Alternatively, add the connector without the plugin:

```
claude mcp add --transport http ecommiq https://ecommiq.tools/api/mcp/v1/ecommiq
```

## What Claude can do

- List the companies and data sources your account can access.
- Find which EcommIQ report covers a question, where it sits in the sidebar, and which metrics
  and filters it supports.
- Answer questions using governed business metrics, so figures match their EcommIQ definitions.
- Run read-only SQL queries against your company's data for ad-hoc analysis, including longer
  queries in the background.
- Report a problem with the connector to the EcommIQ team.

The connector is read-only: it cannot change your data.

## Privacy and security

- Sign-in uses OAuth 2.1 with PKCE. Claude never sees your EcommIQ password.
- Access is checked on every request. If your account or your company's AI access is turned off,
  the connector stops working immediately.
- Query results are returned to Claude as part of your conversation and are subject to your Claude
  plan's data retention settings.

## Support

Ask Claude to "report an issue with EcommIQ", or contact your Digital Fuel Capital team.

## License

[MIT](LICENSE)
