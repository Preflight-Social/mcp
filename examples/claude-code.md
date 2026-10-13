# Claude Code

```bash
claude mcp add --transport http preflight https://preflight.social/mcp
```

Then run `/mcp` inside Claude Code and follow the browser sign-in (OAuth 2.1 with PKCE).

With an API key instead of OAuth:

```bash
claude mcp add --transport http preflight https://preflight.social/mcp \
  --header "Authorization: Bearer sk_live_..."
```
