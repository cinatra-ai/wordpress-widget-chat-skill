# Cinatra WordPress Widget Chat Skill

The conversational half of Cinatra's in-editor WordPress assistant: it decides when a message is a real edit request and when it is just a question, then explains what changed in plain English instead of pasting raw tool output. Packaged as its own skill so the WordPress connector reaches it through a declared dependency rather than embedding it.

**Install:** Install `@cinatra-ai/wordpress-widget-chat-skill` in your Cinatra instance. `@cinatra-ai/wordpress-mcp-connector` installs it automatically as a declared dependency.

**Usage:** The skill is delivered into the widget chat by the connector that depends on it — you do not invoke it directly. It provides the `widget-chat.wordpress-content-editor` capability, which the connector's widget stream names.

**Configuration:** None. The skill carries no credentials and reads no settings; the connector supplies the content-editor tool and pins the post context server-side.

**Development:** Clone the repository and run `node extension-kind-gate.mjs --package-root .` to validate the manifest. The bundle lives in `skills/wordpress-widget-chat/`.

**Troubleshooting:** If the widget answers but never edits, the content-editor tool is not reaching the run — check the connector's widget stream. If replies contain raw JSON, the bundle is not being mounted and the model is improvising.

## Works with

- Cinatra WordPress MCP connector
- Any extension declaring a skill dependency on this package

## Capabilities

- Separate edit requests from conversation before spending a tool call
- Summarize a content-editor result in plain English, never as raw JSON
- Announce the demote-then-edit behavior when a published post is changed
- Keep replies short enough for a sidebar overlay
- Warn about long-running edits without prefacing trivial ones
