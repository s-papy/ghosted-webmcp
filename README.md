# Roach Motel Exit

A subscription dashboard where canceling by hand gets you the real "Roach
Motel" maze — a retention offer, a guilt step, a mandatory reason — while an
agent using this page's WebMCP tools cancels in one call. Entry for
**[The WebMCP Challenge](https://webmcp.devpost.com/)** (deadline 3 September
2026, 1pm PDT).

**Live demo:** https://s-papy.github.io/roach-motel-exit-webmcp/
**Video:** _add the YouTube link here_

## Why WebMCP is a strong fit

The average subscriber hits **6.2 dark patterns and 6.7 clicks** to cancel a
service — well-documented enough that the US FTC built a
["Click to Cancel"](https://www.ftc.gov/legal-library/browse/rules/negative-option-rule)
rule around it. Cancellation flows are hard on purpose: the real cancel
button is buried behind a retention offer, a "are you sure" guilt step, and a
mandatory reason field.

An agent trying to help here can't just guess at the DOM — it would hit the
same maze a human does, or worse, get tricked into accepting the retention
offer by mistake. WebMCP fixes this at the source: the page tells the agent
the truth about what "cancel" means through a `cancel_subscription` tool that
*is* the real exit, not a UI element that can be hidden behind three modals.
When a human clicks Cancel, they get the maze (openly, so you can feel what
it's simulating). When an agent calls the tool, it skips straight to done —
and you watch the card update on the same page, in real time.

## The tools

| Tool | Read-only? | What it does |
|---|---|---|
| `list_subscriptions` | yes | List all subscriptions, optionally filtered by status. |
| `get_subscription` | yes | Full detail on one subscription, matched by id or name. |
| `search_subscriptions` | yes | Filter by text, category, or status. |
| `get_savings_summary` | yes | Monthly spend, spend on unused subscriptions, potential annual savings. |
| `cancel_subscription` | no | Cancel immediately, matched by id or name — no retention flow. |
| `pause_subscription` | no | Pause instead of canceling outright. |

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

Everything lives in the browser's own `localStorage` — six demo
subscriptions with real-world brand names as illustrative example data, no
real accounts, no real money, no connection to any real service. This
project is not affiliated with or endorsed by any company named on the page.
Nothing is sent to a server; there is no server. Clearing site data resets
the board.

## License

MIT — see [LICENSE](LICENSE).
