# SlideForge

Cursor plugin that connects agents to [SlideForge](https://www.slideforge.io)
through SlideForge's official remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

Generate PowerPoint presentations from a topic or brief, then export them as
PPTX or PDF.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **SlideForge**.
3. Click **Install**, then complete the SlideForge sign-in prompt.

Or run `/add-plugin slideforge` in chat.

## MCP

```json
{
  "mcpServers": {
    "slideforge": {
      "type": "http",
      "url": "https://mcp.slideforge.io/mcp"
    }
  }
}
```

Auth is OAuth 2.1 with PKCE. Cursor prompts you to sign in to SlideForge
(email, Google, or Apple) when the plugin connects. There is no client ID or
API key to configure.

## Before you connect

You need a SlideForge account. You can create one on the sign-in screen. New
accounts start a 7-day free trial ($0 today) before their first presentation.
Each slide generated uses one slide from your account's balance.

## What agents can do

| Tool | What it does |
| --- | --- |
| `generate_presentation` | Start a presentation from a topic, with slide count, tone, audience and language |
| `check_presentation_status` | Poll a presentation until it's completed |
| `export_presentation` | Get a download link for PPTX, PDF, or slide images |
| `list_presentations` | List your presentations |
| `list_templates` | List available templates |
| `get_account` | Show your slide balance and plan |

The hosted server is the source of truth for tool names and schemas.

## Skills

- `create-presentation`: turns a request (or this project's docs) into a
  brief, generates the deck, waits for it and returns a download link.

## Notes

- Generation is asynchronous: `generate_presentation` returns an id that the
  agent polls until it's complete.
- Download links are short-lived. Export again if one expires.

## Docs

- SlideForge MCP server: https://www.slideforge.io/mcp
- Server URL: https://mcp.slideforge.io/mcp
- Support: contact@slideforge.io

## License

MIT
