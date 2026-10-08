---
name: search
description: Find notes in the user's Stash notebook by keyword. Use when they want a specific note, a title, a tag, or a list of matches. Do not use for an open question across many notes; use ask for that.
---

# Search Stash notes

Works on free and Pro accounts. Search runs on the server over the signed-in user's decrypted notes.

## Steps

1. Call `stash_search` with a short keyword query (a name, place, tag, or title), not a long question. Use `limit` only when they asked for a longer list.
2. Show the matching titles, ids, and summaries the tool returned. If nothing matches, say so.
3. Call `stash_get` before quoting a note's body. Quote only text the tool returned.
4. If several notes match, list them and ask which one to open. Do not pick one and pretend it was the only hit.

## Do not

- Do not invent notes, ids, titles, or quotations that search did not return.
- Do not call `stash_create` from a search. Saving a new note is the summarize skill.
- Do not call `stash_delete` or `stash_update` from a search result unless the user names that note and confirms.
