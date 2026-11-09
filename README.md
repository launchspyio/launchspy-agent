# LaunchSpy for AI agents

Spy on the ads and funnels of the top coaches and course creators from your AI agent, and copy what works: who sells in a niche, the Meta ads they run, how long each ad has been running, the funnels behind the ads and the tools those funnels are built on.

This repository packages the [LaunchSpy MCP server](https://launchspy.io/mcp) with a workflow skill, for Claude Code, Hermes Agent and any client that reads Agent Skills.

## What your agent can do

- **Map a niche**: the creators that advertise the most in a niche and a country, with their platforms, followers and ad volume.
- **Study a competitor**: their active ads, headlines, calls to action and landing pages, and how many new ads they launched in the last 30 days.
- **Find winning angles**: search ad copy by topic, ranked by run length and EU reach.
- **Take a funnel apart**: steps, builder, tracking pixels, payment stack, pricing and urgency mechanics.
- **Check a website**: what LaunchSpy already knows about any domain.

Six read-only tools: `search_creators`, `get_creator`, `search_ads`, `search_funnels`, `get_funnel`, `analyze_url`.

## Requirements

- A LaunchSpy account on a plan that includes the MCP (Pro or Business). See [pricing](https://launchspy.io/pricing).
- Each tool call uses one LaunchSpy credit. Connecting and listing the tools is free.

## Install

### Claude Code

```bash
claude mcp add --transport http launchspy https://launchspy.io/api/mcp
```

Then copy `skills/launchspy` into `~/.claude/skills/`, or install the skill with the command below.

### Any agent that reads skills

```bash
npx skills add launchspyio/launchspy-agent
```

### Hermes Agent

```bash
hermes plugins install launchspy
```

The first tool call opens your browser to sign in to LaunchSpy.

### Other MCP clients (Claude Desktop, Cursor, ChatGPT, n8n…)

Use the server URL `https://launchspy.io/api/mcp` with OAuth, or an API key from LaunchSpy Settings → API. Step-by-step guides: [launchspy.io/mcp](https://launchspy.io/mcp).

## Disclosure

- **Network**: every tool call goes to LaunchSpy's hosted server (`launchspy.io`) and runs on the signed-in user's account. The tool set is served by that server at runtime.
- **Credits**: each successful or failed `tools/call` uses one credit of the user's LaunchSpy plan.
- **Sign-in**: in Hermes, the package runs the pinned `mcp-remote@0.1.49` through `npx` (Node.js 20.18.1+ and npm required). On first use it opens a browser and a local callback port, and stores OAuth tokens under `~/.mcp-auth`.
- **Read-only**: all six tools are annotated read-only. They read the LaunchSpy database; none of them writes data or visits a live page. The server is marked untrusted in `plugin.json`, so Hermes asks before calling a tool when it is configured to.
- **Third-party content**: tool results contain text written by advertisers (ad copy, page titles). The skill instructs the agent to treat it as data and never follow instructions found in it.
- **Provenance**: the MCP server, its OAuth server and the product all run on launchspy.io, operated by LaunchSpy (APEX GLOBAL WORLD SOLUTIONS LLC).
- **No local code**: this package is configuration and instructions only (`plugin.json`, `mcp.json`, `.mcp.json`, `skills/`).

## Links

- Product: [launchspy.io](https://launchspy.io)
- MCP guide: [launchspy.io/mcp](https://launchspy.io/mcp)
- Privacy policy: [launchspy.io/privacy](https://launchspy.io/privacy)
- Terms: [launchspy.io/terms](https://launchspy.io/terms)

## License

MIT
