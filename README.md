# Stash

Stash is an AI notebook for iPhone. Share anything into it, such as a link, a screenshot, a photo, or a rough thought, and the Stash server turns it into a structured note with a title, summary, sections, tags, and sources. This plugin lets Claude read and add to that notebook.

## What you can do

- **Search your notes.** "Find what I saved about the Hawaii trip."
- **Open a note.** Claude reads the summarized note before quoting it.
- **Save a note.** "Stash this: renew the car registration next month." The server summarizes it once, in the background.
- **Ask across your notes** (Stash Pro). "What did I save about flights?" Answers come only from your notes, with no web search.

| Skill | Tools it calls |
| --- | --- |
| `search` | `stash_search`, `stash_get` |
| `summarize` | `stash_create`, `stash_get` |
| `ask` | `stash_ask` |

The server also exposes `stash_me`, `stash_update`, `stash_delete`, and `stash_research`. The skills only update or delete a note when you name that note and confirm.

## Setup

1. Get Stash from the [App Store](https://apps.apple.com/us/app/stash-ai-notes/id6790027107) and sign in with Apple or Google.
2. Install this plugin. The first time Claude calls a Stash tool, it opens a Stash sign-in page. Use the same Apple or Google account as the app.
3. On the consent screen, review the scopes and select **Allow**.

Free accounts can search, read, and save notes. A free account gets 30 summaries and 5 research reports per month, resetting on the 1st (UTC). Ask needs Stash Pro.

## What this plugin runs and sends

This plugin has no local code. It declares one remote MCP server, `https://stash.graftedsoftware.com/mcp`, run by Grafted Software, plus three skills written in Markdown.

- Claude sends tool calls (search queries, note text you ask it to save, note ids) to that server, authenticated with an OAuth token you grant on the consent screen.
- Notes are encrypted at rest (AES-256-GCM). They are not zero-knowledge: the server decrypts them to run tools, the same way it already does to summarize a note.
- To summarize, research, and answer questions, the server sends note text to Anthropic (Claude), via OpenRouter. Summaries and research also use OpenRouter's web search. To decide whether a summary should use web search, it sends up to 2,000 characters of the note to TypeSafe (Jev), via OpenRouter.
- Audit logs record the action, note id, and client id. They never record note bodies or search text.

To stop access, remove the connector in Claude or delete your Stash account in the app.

## Privacy and support

- Privacy policy: <https://stash.graftedsoftware.com/legal/privacy>
- Terms: <https://stash.graftedsoftware.com/legal/terms>
- Agent docs: <https://stash.graftedsoftware.com/agents>
- Support: <support@graftedsoftware.com>

## License

MIT. See [LICENSE](./LICENSE).
