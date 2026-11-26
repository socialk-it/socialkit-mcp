# SocialKit MCP

[SocialKit](https://socialk.it) is a social media scheduler. Its remote MCP server lets an AI app write, schedule and check posts on 11 networks and read analytics in your SocialKit account.

Server URL (Streamable HTTP):

```
https://app.socialk.it/core/mcp
```

Official MCP registry name: `it.socialk/socialkit`.

The server is hosted by SocialKit and its code is closed source. This repository holds only the client manifests and the docs.

## What it does

32 tools, grouped like this:

- Workspaces and accounts: list your workspaces and connected accounts, see what each account can do, list or create Pinterest boards.
- Posts: list, read, create, update, duplicate, delete and restore posts, and edit or remove the version for one network.
- Schedule: schedule or unschedule a post, add it to the queue, find the best posting times.
- Media: list media, upload from a public link, check an upload.
- Tags: list, create and update tags, attach them to posts or remove them.
- Analytics: a summary, per account and per post.

Networks: X, LinkedIn, Facebook, Instagram, TikTok, YouTube, Pinterest, Threads, Bluesky, Mastodon and Google Business Profile.

It works with your role in SocialKit. A post that needs approval waits for it.

## Sign in

- OAuth 2.1 with PKCE, scope `mcp`. Client ID Metadata Documents and Dynamic Client Registration are supported. Apps that sign in this way open a browser window where you sign in to SocialKit and click Allow access. There is no key to copy.
- Or a personal key sent as `Authorization: Bearer YOUR_PERSONAL_KEY`. Create it at [app.socialk.it](https://app.socialk.it), user menu, API.

You need a SocialKit account. There is a 7-day free trial.

## Connect your app

Every app uses the same server URL. Each page below has the steps, plan notes and prompts to copy.

| App | How | Steps |
|---|---|---|
| Claude | Customize > Connectors > Add custom connector, paste the URL, sign in | [socialk.it/en/mcp/claude](https://socialk.it/en/mcp/claude) |
| ChatGPT | chatgpt.com/plugins > Add custom MCP server, choose OAuth. Full use needs Business, Enterprise or Edu | [socialk.it/en/mcp/chatgpt](https://socialk.it/en/mcp/chatgpt) |
| Cursor | Plugin from this repo, or the `mcp.json` below | [socialk.it/en/mcp/cursor](https://socialk.it/en/mcp/cursor) |
| VS Code | Chat: Open Customizations > MCP Servers > Add Server, HTTP, paste the URL, sign in | [socialk.it/en/mcp/vs-code](https://socialk.it/en/mcp/vs-code) |
| Claude Code | One command with a personal key (below) | [socialk.it/en/mcp/claude-code](https://socialk.it/en/mcp/claude-code) |
| Gemini CLI | Extension from this repo, or one command with a personal key (below) | [socialk.it/en/mcp/gemini](https://socialk.it/en/mcp/gemini) |

More apps (Codex, Windsurf, Grok, Perplexity, Notion, n8n, Zapier, Make and others) are listed at [socialk.it/en/mcp](https://socialk.it/en/mcp).

### Claude Code

```bash
claude mcp add --transport http --scope user socialkit https://app.socialk.it/core/mcp \
  --header "Authorization: Bearer YOUR_PERSONAL_KEY"
```

The browser sign-in of Claude Code does not work with SocialKit today, so use the key.

### Cursor

Add to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project) with a personal key read from an environment variable:

```json
{
  "mcpServers": {
    "socialkit": {
      "url": "https://app.socialk.it/core/mcp",
      "headers": {
        "Authorization": "Bearer ${env:SOCIALKIT_KEY}"
      }
    }
  }
}
```

Sign-in in the browser from Cursor is not confirmed yet. The key is the sure way.

### Gemini CLI

```bash
gemini mcp add --scope user --transport http --header "Authorization: Bearer YOUR_PERSONAL_KEY" socialkit https://app.socialk.it/core/mcp
```

Or install this repository as an extension. Gemini CLI asks for your personal key during install:

```bash
gemini extensions install https://github.com/socialk-it/socialkit-mcp
```

## Files in this repository

| File | Used by |
|---|---|
| `server.json` | The [official MCP registry](https://registry.modelcontextprotocol.io) |
| `.cursor-plugin/plugin.json` and `mcp.json` | Cursor plugin |
| `gemini-extension.json` | Gemini CLI extension |

## Links

- Docs: [socialk.it/en/mcp](https://socialk.it/en/mcp)
- Privacy: [app.socialk.it/pages/privacy](https://app.socialk.it/pages/privacy)
- Terms: [app.socialk.it/pages/terms](https://app.socialk.it/pages/terms)
- Support: contact@socialk.it

## License

[MIT](./LICENSE). The license covers the files in this repository, not the SocialKit service.
