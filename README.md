# Tiny Kanban

A tiny, local-first kanban board in one HTML file.

Open `Kanban.html` in a browser and use it directly. No server, account, build step, or cloud sync required.

The app loads React, ReactDOM, Babel Standalone, and the DM Sans font from CDNs, so first launch needs internet access unless those files are already cached by the browser.

![Tiny Kanban light theme](screenshots/tiny-kanban-light.png)

![Tiny Kanban dark theme](screenshots/tiny-kanban-dark.png)

## What It Does

- Drag cards and columns
- Rename and recolor columns
- Edit cards, notes, labels, checklists, deadlines, and local attachments
- Show unfinished checklist items on card previews
- Reorder checklist items and labels
- Filter by labels
- Sort the whole board or one column by due date
- Import/export board JSON, or start a new blank board
- Optional auto-backup to a local JSON file with a previous-copy backup
- Optional local file/image attachments per card, with image previews when available
- Dark and light themes

## Running on Windows

From File Explorer, double-click `Kanban.html`.

From PowerShell:

```powershell
Start-Process .\Kanban.html
```

Chrome or Edge is recommended if you want Auto Backup or file picker features, because those depend on the File System Access API. Other modern browsers can still use the board, `localStorage` autosave, and manual import/export fallback behavior.

## Development

There is no build step, package manager setup, local server, or npm project. The tracked application code is in `Kanban.html`.

The current implementation is intentionally small and dependency-light:

- CSS lives in the `<style>` block near the top of `Kanban.html`.
- React app code lives in the `<script type="text/babel">` block near the bottom.
- Board data is saved as schema version `2` under `localStorage` key `kb-v2`.
- Older `kb-v1` data is migrated on load.
- Auto Backup and attachment handles are stored through IndexedDB and browser file handles.

## Testing

There are no automated tests, lint commands, or build checks.

Use this manual smoke test before shipping changes:

1. Open `Kanban.html` in Chrome or Edge.
2. Add a card, edit its title and notes, then reload and confirm it persisted.
3. Drag a card between columns and drag a column to reorder it.
4. Add, rename, recolor, reorder, filter by, and remove labels.
5. Add checklist items, reorder them, toggle them, and confirm card previews update.
6. Set due dates and sort one column and the whole board by due date.
7. Export JSON, create a new board, import the JSON, and confirm the board returns.
8. Try Auto Backup in Chrome or Edge and confirm the live and previous JSON files update.
9. Add an image attachment, confirm its preview appears, reload, and try opening it.
10. Toggle dark/light theme and reload.

## Storage

The board autosaves to browser `localStorage`. For safer storage, use `Backup > Auto Backup` to choose a local JSON backup file.

Local attachments are browser-local file handles. Exported JSON keeps attachment metadata, but another browser or machine may need files re-added.

## Permissions

Auto Backup uses the browser's local file access features.

Your browser will ask for permission to edit the chosen JSON file. Folder-based backup will also ask for access to the backup folder so Tiny Kanban can update the live backup and previous copy. Chrome may describe this as `file:/// can edit the following files and folders`. You can remove this access at any time.

Reloading the page does not affect Auto Backup. Closing the page and opening it again will make the browser re-request permissions to edit the local JSON file. 

Auto Backup is fully optional. If you do not want to grant extra file permissions, the board still autosaves in the browser and manual import/export still works. No additional permissions needed.

## Review Notes

The most sensitive areas are persistence, import/migration, backup permissions, attachments, and drag/drop behavior. Avoid changing storage keys, JSON schema, backup semantics, or attachment behavior unless you have a specific migration or compatibility plan.

Local `*.json` files are ignored by git and are treated as personal board data or backups.

## Files

- `Kanban.html` - the app
- `icon.ico` - browser tab icon
- `screenshots/` - README screenshots
- `LICENSE` - project license
- `.gitignore` - ignores local board JSON backups
