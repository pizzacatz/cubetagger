Web app url (https://pizzacatz.github.io/cubetagger/)


# MTG Tag Builder (Offline CSV Tool)

A single-file, offline HTML web app for efficiently tagging **Magic: The Gathering** cards using a semicolon-delimited tag system stored in a CSV file.

This tool is designed for **fast, low-friction categorization** while preserving full control over your data. No backend. No dependencies. Just open the file in Chrome.

---

## What This Tool Does

- Imports a CSV file with **exact headers**:
  - `name`
  - `tags`
- Displays each card (row) one at a time
- Lets you assign tags using a **clickable bubble grid**
- Automatically writes tag changes back to the active row
- Supports **duplicate card names** safely via row index tracking
- Exports a **new updated CSV** when finished

---

## Core Concepts

### Tags
- Tags are **semicolon-separated**:  
- No spaces, no trailing semicolon
- Tags are normalized to **Title Case**
- Deduplicated case-insensitively

### Tag Universe
The **Universe** is the master list of all possible tags shown in the grid.

It is built as:
- the **union of all tags found in the imported CSV**, plus
- any **new tags added via typing + Build/Apply**

Important behaviors:
- Universe is **global to the dataset**
- Universe is **always sorted alphabetically**
- Universe **resets completely** when a new CSV is imported
- Removing tags from Universe is done implicitly by re-importing a CSV without them

This makes CSV import a clean, predictable “reset” mechanism.

---

## Workflow (Recommended)

1. Open the HTML file in **Chrome**
2. Import a CSV (`name`, `tags` headers required)
3. For each card:
 - Read card name (large display)
 - Toggle tags in the grid (auto-saves to that row)
 - Optionally type new tags and click **Build/Apply**
4. Click **Next** at the bottom to move forward
5. When finished, click **Download updated CSV**

Your original CSV is never modified.

---

## UI Layout Philosophy

Top → Bottom flow per card:

1. **CSV Import** (top, done once)
2. **Current Card Name** (large, adjustable font)
3. **Input / Output / Tag Grid** (primary work area)
4. **Navigation + Download** (bottom)

This minimizes scrolling and keeps actions aligned with reading order.

---

## Persistence

- Dataset, Universe, per-row drafts, and UI state are saved to `localStorage`
- Closing and reopening the file restores your session
- Importing a new CSV replaces the current dataset and Universe

---

## CSV Requirements (Intentional Brittleness)

This app is intentionally strict.

Your CSV **must**:
- Use exact lowercase headers: `name`, `tags`
- Use semicolon-delimited tags in the `tags` column

Extra columns are allowed and preserved untouched.

If the headers do not match exactly, the import will fail.

---

## Limitations (By Design)

- Cannot overwrite the original CSV file (browser sandbox)
- Universe only exists within the currently loaded CSV
- No tag deletion UI (reset via re-import instead)
- No fuzzy matching or tag taxonomy enforcement

These constraints keep the tool simple, predictable, and safe.

---

## Why This Exists

This tool prioritizes:
- **Completion over perfection**
- **Speed over abstraction**
- **Data clarity over configurability**

It is meant to support creative classification work without becoming a project in itself.

---

## License

MIT — use, modify, share freely.

---

## Usage Notes

- Best used in **Chrome (desktop)**
- Clipboard features may be restricted in some environments
- Keep exported CSVs as checkpoints if you experiment aggressively

---

If you find yourself wanting tag pruning, presets, or multi-CSV consistency, those are valid future extensions — but this version is intentionally scoped to stay lightweight.
