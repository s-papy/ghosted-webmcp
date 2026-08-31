# Ghosted

A tracker that admits when someone's gone silent — a job application, or an
unpaid freelance invoice — instead of leaving you to guess. An agent using
this page's WebMCP tools can log things the moment they happen and flag every
stale one in a single call. Entry for
**[The WebMCP Challenge](https://webmcp.devpost.com/)** (deadline 3 September
2026, 1pm PDT).

**Live demo:** https://s-papy.github.io/ghosted-webmcp/
**Video:** _add the YouTube link here_

## Why WebMCP is a strong fit

53% of job seekers were ghosted by an employer in the past year, and it now
takes roughly 40 applications to land one interview. Existing trackers (Teal,
Huntr, spreadsheets) are passive organizers — you copy each application in by
hand after the fact, then check dates one by one to guess who's gone quiet.

An agent can do both parts of that chore for real: log the application in the
same breath as helping you apply, and later, in one tool call, flag every
application that's gone 21+ days without a response — work that's tedious to
do by hand across dozens of applications and easy to keep putting off. This
only works because the page exposes real, callable actions instead of a UI
the agent would have to guess at, and because the state is shared: what the
agent logs or flags shows up on the same page you're looking at, immediately.

Paid trackers sell "salary negotiation" as a static column you have to
remember to check. Here it's a live cross-reference: the moment one
application reaches offer stage, the page surfaces which other still-active
applications are worth notifying about the competing offer — computed from
the same shared state, not a feature you have to go looking for.

It also tracks a real personal benchmark — average response time — the same
kind of KPI industry ghosting research uses, computed automatically from your
own data instead of a number you'd have to calculate by hand.

The same shape of problem shows up for freelancers: 85% get paid late, and
they're owed $6,000 in unpaid invoices on average — they lose over a full
workday a month just chasing clients. It's the identical mechanic applied to
a second, equally real kind of silence: `flag_stale_invoices` marks every
overdue invoice with no response as ghosted in one call, the same way
`flag_stale_applications` does for job applications, because being ignored
by an employer and being ignored by a client are the same problem wearing a
different name.

A `get_daily_digest` tool spans both boards in a single call — stale items,
follow-ups worth sending, any offer worth leveraging — the kind of "what
actually needs me today" view that would otherwise take an agent several
separate calls across two unrelated trackers.

## The tools

**Job applications**

| Tool | Read-only? | What it does |
|---|---|---|
| `log_application` | no | Log a new application (company, role, url, date). |
| `get_application` | yes | Full detail on one application, matched by id or company. |
| `list_applications` | yes | List applications, optionally filtered by status. |
| `search_applications` | yes | Filter by text and/or status. |
| `update_status` | no | Move an application to a new status (interviewing, offer, rejected, ghosted, withdrawn). |
| `flag_stale_applications` | no | Mark every application silent for 21+ days as ghosted, in one call. |
| `get_followup_reminders` | yes | Applications 7-20 days old — the window where following up is still worth it. |
| `get_pipeline_summary` | yes | Total applications, response rate, ghost rate, applications awaiting follow-up. |
| `get_leverage_opportunities` | yes | If any application reached offer stage, list other live applications worth notifying. |

**Freelance invoices**

| Tool | Read-only? | What it does |
|---|---|---|
| `log_invoice` | no | Log a new invoice (client, project, amount, dates). |
| `get_invoice` | yes | Full detail on one invoice, matched by id or client. |
| `list_invoices` | yes | List invoices, optionally filtered by status. |
| `search_invoices` | yes | Filter by text and/or status. |
| `update_invoice_status` | no | Move an invoice to a new status (paid, disputed, ghosted, written off). |
| `flag_stale_invoices` | no | Mark every invoice overdue 21+ days with no response as ghosted, in one call. |
| `get_invoice_followup_reminders` | yes | Invoices 1-20 days overdue — worth a polite reminder before assuming the worst. |
| `get_payment_summary` | yes | Total invoiced, paid, unpaid, amount owed by ghosted clients, late-payment rate, average payment delay. |

**Cross-domain**

| Tool | Read-only? | What it does |
|---|---|---|
| `get_daily_digest` | yes | One call spanning both trackers: stale items, follow-ups worth sending, and any offer worth leveraging. |

## Running it

Single static file — no build step, no backend, no dependencies.

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Or deploy `index.html` as-is to any static host (Vercel, Netlify, Cloudflare
Pages, GitHub Pages, ...).

To test the WebMCP tools:

- **Chrome**: enable `chrome://flags/#enable-webmcp-testing`, relaunch, then
  open the page and talk to an agent that supports WebMCP (e.g. the
  [Model Context Tool Inspector](https://chromewebstore.google.com/detail/model-context-tool-inspec/gbpdfapgefenggkahomfgkhfehlcenpd)
  extension).
- **ChatGPT**: open the deployed URL in ChatGPT's in-app browser.

## Data & privacy

Everything lives in the browser's own `localStorage` — eight demo
applications and seven demo invoices with fictional company/client names, no
real inbox access, no real job board or bank connection. Nothing is sent to
a server; there is no server. Clearing site data resets the board.

## License

MIT — see [LICENSE](LICENSE).
