# earmarkIQ MCP server

Read-only access to your own UK bank data from any MCP client: spending, subscriptions, payday plan, net worth.

**Server URL:** `https://api.earmarkiq.app/mcp` (Streamable HTTP, remote only)  
**Auth:** OAuth 2.1 with dynamic client registration and PKCE. Sign in with your earmarkIQ account. No API keys.  
**Registry:** `app.earmarkiq/earmarkiq` on the [official MCP Registry](https://registry.modelcontextprotocol.io/v0.1/servers?search=app.earmarkiq/earmarkiq)  
**Website:** [earmarkiq.app](https://earmarkiq.app) · [Privacy](https://earmarkiq.app/privacy) · [Terms](https://earmarkiq.app/terms)

This repository holds the public documentation and registry manifest for the server. The server itself is a hosted service and is not open source.

## What it does

earmarkIQ is a UK budgeting app built on Open Banking. Connect your current accounts, savings and credit cards in the app, then connect the MCP server to Claude, Cursor, VS Code or any other MCP client and ask about your own money:

- "What did I spend on groceries last month compared with the month before?"
- "List my subscriptions and flag any that went up in the last 12 months."
- "How much can I safely spend before my next payday?"
- "What is my net worth right now, and how much of it is my pension?"
- "Which merchant did I pay most often in the last 90 days?"

Everything is read-only. The server cannot initiate payments, move money, change settings, or see your bank login.

## Tools

All seven tools are read-only and annotated `readOnlyHint: true`.

| Tool | Returns |
| --- | --- |
| `get_accounts` | Connected accounts and balances |
| `get_transactions` | Transactions, with date, merchant, category and amount filters |
| `get_spending_summary` | Spending by category for a period |
| `get_subscriptions` | Recurring payments and subscriptions, including price changes |
| `get_payday_summary` | Income, committed outgoings and safe-to-spend until the next payday |
| `get_net_worth` | Assets and liabilities, including property equity |
| `get_investments` | Investment and pension holdings |

## Connecting

You need an earmarkIQ account with at least one bank connected ([App Store](https://apps.apple.com/app/id6759535975) or [my.earmarkiq.app](https://my.earmarkiq.app)).

**Claude (web or desktop):** Settings → Connectors → Add custom connector → URL `https://api.earmarkiq.app/mcp` → sign in when prompted.

**Claude Code:**

claude mcp add --transport http earmarkiq https://api.earmarkiq.app/mcp


**Cursor / VS Code / other clients:** add a remote MCP server with the URL above. The server advertises its OAuth resource metadata, so clients that support OAuth 2.1 discovery will open the sign-in flow automatically.

Example `mcp.json`:
```json
{
  "mcpServers": {
    "earmarkiq": {
      "url": "https://api.earmarkiq.app/mcp"
    }
  }
}
```

## Data and regulation

earmarkIQ Ltd is an agent of Finexer Limited, which is authorised and regulated by the Financial Conduct Authority (FRN 925695) for account information services. Bank connections are read-only and consented by you; your bank login is never shared with earmarkIQ. You can disconnect a bank or revoke the MCP client's access at any time from the app. See the [privacy policy](https://earmarkiq.app/privacy).

## Pricing

Plus from £4.99 a month, Pro from £9.99, with a 7-day free trial on Pro. The MCP server is included with a paid plan.

## Support

caolan.preston@earmarkiq.com
