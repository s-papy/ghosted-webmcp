# Cash Pipeline

A board of grants, hackathons and freelance leads that a person and their AI
agent can both read and edit — live, on the same page. Entry for
**[The WebMCP Challenge](https://webmcp.devpost.com/)** (deadline 3 September
2026, 1pm PDT).

**Live demo:** _add the deployed URL here after publishing_
**Video:** _add the YouTube link here_

## Why WebMCP is a strong fit

Tracking cash opportunities (apply-for-a-grant, join-a-hackathon,
freelance-lead) is a chore an agent is well suited to help with — it can spot
a new opportunity while researching the web and log it, or check in on
deadlines — but only if it can act on the *same* data a human is looking at,
not a private copy it can't be checked against.

This page keeps one shared list in `localStorage` and exposes it two ways at
once:

- **A human UI** — a table, a filter bar, an "add" dialog.
- **Six WebMCP tools** (`document.modelContext.registerTool`) — `add_opportunity`,
  `update_status`, `remove_opportunity`, `get_deadlines`,
  `get_pipeline_summary`, `search_opportunities`.

Both paths call the same `load()` / `save()` / `render()` functions. When the
agent adds a lead through a tool call, it appears in the table immediately —
the human doesn't have to trust a claim, they watch it happen. When the human
edits a row by hand, the next tool call the agent makes reads the update. That
shared, visible state is what WebMCP is for: not an agent doing something to a
page, but a person and an agent working the same board.

What was difficult before: an agent without WebMCP would have had to guess at
DOM structure to scrape or fill this table (fragile, and invisible to the
person until it broke), or maintain its own private notes disconnected from
what the person actually sees.

## The tools

| Tool | Read-only? | What it does |
|---|---|---|
| `add_opportunity` | no | Add a lead (name, url, type, deadline, amount, status, notes). |
| `update_status` | no | Move a lead between spotted / in_progress / submitted / won / rejected, matched by id or name. |
| `remove_opportunity` | no | Delete a lead, matched by id or name. |
| `get_deadlines` | yes | Open leads sorted by nearest deadline. |
| `get_pipeline_summary` | yes | Counts by status, total open cash, nearest deadline. |
| `search_opportunities` | yes | Filter by text, type, or status. |

## Running it

It's a single static file — no build step, no backend, no dependencies.

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

Everything lives in the browser's own `localStorage`. Nothing is sent to a
server — there is no server. Clearing site data clears the board.

## License

MIT — see [LICENSE](LICENSE).
