# Quotelyfy MCP Server

Connect Claude to your Quotelyfy workspace and run your business in plain language — ask what is owed, raise a quote, move a job along, chase an invoice, add to your planner. Quotelyfy is a business operating system for small businesses (quotes, invoices, jobs, projects, expenses and payments), and this is its remote MCP server: a hosted connector you add once, with no install and nothing to run locally.

> **Remote server.** There is no package to install. Point your client at the URL below and sign in — the OAuth flow issues the credentials for you.

```
https://api.quotelyfy.com/mcp
```

## What you can ask it

- *"Which invoices are due this week, and what are they worth?"*
- *"Create a quote for Acme for 3 signs at R5,660 each and email it."*
- *"Move job QTL-ORD-4647 to Bags Tagged and tell the team."*
- *"What is overdue, oldest first?"*
- *"Add a planner item to chase the Maswanganyi deposit on Friday."*

## Connecting

### Claude (web, desktop)

1. **Customize → Connectors → + Add → Add custom connector**
2. Name it `Quotelyfy` and paste the URL above, then **Continue**
3. Leave the authentication settings as discovered and **Continue**
4. Choose **Sign in now**, sign in to Quotelyfy and approve access
5. Pick the company you want Claude to work in

On Team and Enterprise plans a connector is added once by an Owner under
**Organization settings → Connectors**; everyone else then presses **Connect**
on it under **Customize → Connectors**.

### ChatGPT

1. Turn on **Developer mode** (Settings → Plugins → Developer mode)
2. **Plugins → + → Add custom MCP server**
3. Paste the URL above, tick the risk acknowledgement and **Create**
4. **Sign in with Quotelyfy** and approve access

### Claude Code / any MCP client

```jsonc
{
  "mcpServers": {
    "quotelyfy": {
      "type": "http",
      "url": "https://api.quotelyfy.com/mcp"
    }
  }
}
```

## Authentication

OAuth 2.1 with PKCE and Dynamic Client Registration (RFC 7591), advertised through
protected-resource metadata (RFC 9728) — so a compliant client discovers everything it
needs from the URL alone and no key is ever pasted anywhere.

| Endpoint | Purpose |
| --- | --- |
| `/.well-known/oauth-protected-resource` | Resource metadata |
| `/.well-known/oauth-authorization-server` | Authorization server metadata |
| `/api/v1/mcp/oauth/register` | Dynamic client registration |

Access is scoped to one company at a time. If your login reaches several, ask Claude to
list them and choose — the choice lasts for that conversation and never changes the
company open in the Quotelyfy web app.

## Tools

Ninety-four tools across the workspace:

| Area | Examples |
| --- | --- |
| Quotes & invoices | create, update, send by email or WhatsApp, mark paid, convert, payment links |
| Jobs / orders | create, move stage, comment, checklist, pin |
| Proposals | draft, send, track status, attach documents |
| Customers & leads | list, update, tag in bulk, lead groups |
| Planner | items, steps, notes, completion |
| Expenses | record, update, mark paid |
| Reporting | dashboard, order counts, invoices due / unpaid / overdue |

Which plans include the connector, and which of its actions, is set out on the
[pricing page](https://quotelyfy.com/pricing). Plans change over time, so it is kept there
rather than here.

## Requirements

- A Quotelyfy account — https://quotelyfy.com
- A Quotelyfy plan that includes the AI connector (see https://quotelyfy.com/pricing)
- An MCP client that supports remote servers with OAuth

## Support

- Product: https://quotelyfy.com
- Help: hello@quotelyfy.com

## About this repository

Documentation and connection details for the hosted Quotelyfy MCP server. The server
itself is a managed service; there is no source to install here, which is the normal
shape for a remote MCP connector. The documentation in this repository is MIT licensed;
the Quotelyfy service itself is proprietary and governed by its own terms.


## Anthropic badge
<a href="https://www.claudeai.directory/launches/quotelyfy" target="_blank" rel="noopener"><img src="https://www.claudeai.directory/badge/quotelyfy" alt="Quotelyfy - Listed on Claude AI Directory" width="220" height="54" /></a>
