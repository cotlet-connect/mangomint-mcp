# How to connect Mangomint to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Mangomint account.** Mangomint has no public API and no official MCP server, only outbound webhooks. Cotlet.dev connects your own signed-in Mangomint account to any AI agent, so you can ask in plain words and the AI books, checks and replies for you.

## What you can ask

> Book Anna Kowalski for a balayage with Sam on Friday at 2 pm and text her the confirmation.

> What does tomorrow look like per stylist? List gaps longer than an hour.

> Reply to the unread client messages in the inbox. Show me the drafts first.

> Which clients haven't booked in 90 days? Make a list with their last service.

> Move all of Jess's Saturday appointments to Kim and tell the clients.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Mangomint tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"mangomint":{"command":"uvx","args":["mangomint-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t mangomint-mcp .
docker run -i --rm -e COTLET_API_KEY mangomint-mcp
```

Tools: `mangomint_guide`, `mangomint_status`, `mangomint_open`, `mangomint_read`, `mangomint_click`, `mangomint_type`, `mangomint_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install mangomint-mcp        # or run it once: uvx mangomint-mcp connect
mangomint-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 mangomint_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 mangomint_agent.py status    # is Mangomint ready in your Cotlet.dev account
python3 mangomint_agent.py guide     # Mangomint screens and sign-in link
python3 mangomint_agent.py read      # open Mangomint, read the page, close the browser
python3 mangomint_agent.py tools     # list Cotlet.dev tools
python3 mangomint_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Mangomint users

**Does Mangomint have an API?**

Mangomint has no public, self-service API. It offers outbound webhooks that send events to other apps, but they can't read or change your bookings. Cotlet.dev works in your Mangomint account directly, so your AI agent can do both.

**How do I connect Mangomint to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Mangomint once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no Mangomint API key.

**Is there a way to use Claude with Mangomint?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own Mangomint account.

**Is there a Mangomint MCP server?**

Mangomint has no official MCP server. Cotlet.dev is a hosted MCP server that works in Mangomint for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [Mangomint on Cotlet.dev](https://cotlet.dev/integrations/mangomint-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=mangomint&utm_content=find)
- [PyPI package mangomint-mcp](https://pypi.org/project/mangomint-mcp/)
- [Glama](https://glama.ai/mcp/servers/cotlet-connect/mangomint-mcp)
- [LobeHub](https://lobehub.com/mcp/cotlet-connect-mangomint-mcp)
- [Odel](https://odel.app/modules/cotlet/mangomint)
- [mcpbeat](https://mcpbeat.com/mcp-servers/cotlet/mangomint/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-mangomint-to-ai-agents-guide)

## Also works with

- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [Milanote MCP](https://github.com/cotlet-connect/milanote-mcp)
- [Partiful MCP](https://github.com/cotlet-connect/partiful-mcp)
- [Contractor Foreman MCP](https://github.com/cotlet-connect/contractor-foreman-mcp)
- [Pixieset MCP](https://github.com/cotlet-connect/pixieset-mcp)
- [GlossGenius MCP](https://github.com/cotlet-connect/glossgenius-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
- [FieldEdge MCP](https://github.com/cotlet-connect/fieldedge-mcp)
- [Phorest MCP](https://github.com/cotlet-connect/phorest-mcp)
- [DINGG MCP](https://github.com/cotlet-connect/dingg-mcp)
- [Invoice Simple MCP](https://github.com/cotlet-connect/invoice-simple-mcp)
- [PhotoShelter MCP](https://github.com/cotlet-connect/photoshelter-mcp)
- [RazorSync MCP](https://github.com/cotlet-connect/razorsync-mcp)
- [ShootProof MCP](https://github.com/cotlet-connect/shootproof-mcp)
- [Invoice2go MCP](https://github.com/cotlet-connect/invoice2go-mcp)
- [Appointy MCP](https://github.com/cotlet-connect/appointy-mcp)
- [Contractor+ MCP](https://github.com/cotlet-connect/contractor-plus-mcp)
- [Teachers Pay Teachers MCP](https://github.com/cotlet-connect/teachers-pay-teachers-mcp)
- [Bloom MCP](https://github.com/cotlet-connect/bloom-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/mangomint-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=mangomint

Start free: https://cotlet.dev/signup?app=mangomint&utm_source=github&utm_medium=readme&utm_campaign=mangomint
