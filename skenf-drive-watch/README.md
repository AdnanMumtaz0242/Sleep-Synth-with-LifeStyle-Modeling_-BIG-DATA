# SKENF Drive Watch Log

Not part of the Sleep-Synth-with-LifeStyle-Modeling analysis. This folder exists only to persist
a running record of new file uploads to the SKENF Google Drive (owned by `skenfnit@gmail.com`),
tracked here because this is the only repo in scope for the Claude Code session doing the watching.

## Files

- `known_files.json` — machine-readable state: a `watermark` (the `createdTime` of the newest
  file already seen) plus a snapshot of recently known files. Each check compares Drive's
  `createdTime` against the watermark to find genuinely new uploads, then advances the watermark.
- `log.md` — human-readable changelog, newest entry on top, of what was found on each check.

## Scope

All files owned by `skenfnit@gmail.com` across the SKENF Drive (not limited to one folder).
Query used: `owner = 'skenfnit@gmail.com' and trashed = false`, filtered client-side on
`createdTime > watermark`, via the `Google_Drive` MCP connector's `search_files` tool.

## Caveats

- This log only advances when a Claude Code session actively checks (manually, or via a
  session-scoped recurring job) and pushes an update — there is no live push notification from
  Drive wired up. See the note left in chat for why, and the native-trigger alternative
  (Drive push notifications / Apps Script `onChange`) if 24/7 coverage without a running session
  is needed.
- `trashed = false` means a file uploaded and then deleted before a check runs will never appear.
