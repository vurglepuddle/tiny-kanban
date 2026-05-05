# Tiny Kanban

A tiny, local-first kanban board in one HTML file.

Open `Kanban.html` in a browser and use it directly. No server, account, build step, or cloud sync required.

## What It Does

- Drag cards and columns
- Edit cards, notes, labels, checklists, and deadlines
- Filter and sort by labels or due dates
- Import/export board JSON
- Optional auto-backup to a local JSON file
- Optional local file/image attachments per card
- Dark and light themes

## Storage

The board autosaves to browser `localStorage`. For safer storage, use `Backup > Auto Backup` to choose a local JSON backup file.

Local attachments are browser-local file handles. Exported JSON keeps attachment metadata, but another browser or machine may need files re-added.

## Files

- `Kanban.html` - the app
- `icon.ico` - browser tab icon
- `.gitignore` - ignores local board JSON backups
