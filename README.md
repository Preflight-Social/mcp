# Preflight MCP server

[![smithery badge](https://smithery.ai/badge/info-pcqw/preflight)](https://smithery.ai/servers/info-pcqw/preflight)

[Preflight](https://preflight.social) is a social media scheduler that checks every post against each network's real publishing rules before it leaves. This repository holds the public description of its hosted MCP server: how to connect, what the tools do, and the registry metadata. The server itself is hosted at `https://preflight.social/mcp`; its source is not in this repository.

- **Networks (12):** YouTube, TikTok, Instagram, Facebook, Threads, LinkedIn, Pinterest, Bluesky, Mastodon, Telegram, Discord, Tumblr.
- **Transport:** Streamable HTTP, `https://preflight.social/mcp`.
- **Auth:** OAuth 2.1 with PKCE and dynamic client registration, or an API key as a bearer token.
- **Tools:** 27. **Plans:** the MCP server, API keys and webhooks are on every plan, Free included.
- **Hosting:** EU. Operator: ADMI ENTERPRISES s.r.o., Brno, Czech Republic.

## Connect

| Client | How |
|---|---|
| Claude (web, desktop) | Customize → Connectors → Add custom connector → `https://preflight.social/mcp` |
| Claude Code | `claude mcp add --transport http preflight https://preflight.social/mcp` ([example](examples/claude-code.md)) |
| ChatGPT | Add a custom MCP server with the URL above |
| Cursor | [`examples/cursor-mcp.json`](examples/cursor-mcp.json) |

Step-by-step guide with the menus of each client: https://preflight.social/docs/mcp

## What the tools do

The tools fall into five jobs.

- **Draft:** `draft_post` puts a text draft in the composer. It cannot publish.
- **Check:** `validate_post` is a dry run of `create_post` with the same arguments. It checks every channel, file, time and network limit and creates nothing.
- **Schedule or publish:** `create_post`, with files through `create_media_upload`, `complete_media_upload` and `get_media`. The bytes never pass through the assistant.
- **Manage:** `list_posts`, `get_post`, `update_post`, `delete_post`, `retry_post`, `edit_published_post`, `delete_published_post`.
- **Learn:** `post_performance`, `post_insights`, `analytics_summary`, `audience`, `list_comments`, `act_on_comment`.

Also: `list_channels`, `next_queue_times`, `list_pinterest_boards`, `create_pinterest_board`, `list_youtube_playlists`, `create_youtube_playlist`, `tiktok_creator_info`, `get_usage`.

Everything an assistant publishes goes through the same checks as the web composer and the REST API, so a post that a network would refuse is stopped before it is sent.

## Scopes

| Scope | Lets the assistant |
|---|---|
| `posts:read` | read channels, posts, comments, figures and usage; run `validate_post` |
| `posts:write` | write drafts, edit or delete posts that have not gone out |
| `posts:publish` | anything that goes live |
| `media:read`, `media:write` | see and upload files |

Publishing is its own scope. A connection without `posts:publish` can still draft.

## Links

- Documentation: https://preflight.social/docs/mcp
- REST API and OpenAPI 3.1: https://preflight.social/documentation, https://preflight.social/openapi.json
- Server card: https://preflight.social/.well-known/mcp.json
- Network limits as open data (CC BY 4.0): https://preflight.social/data/network-limits
- Rules tracker (dated changes to the networks' rules): https://preflight.social/rules/tracker
- Contact: info@preflight.social

## License

The contents of this repository (README, examples, `server.json`) are MIT licensed.
