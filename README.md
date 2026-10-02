# Reasoning Coder

A single-file, no-backend scoring tool for reasoning data across the High Preference and
Low Preference/Control stories, matching the structure of your original spreadsheet
template. Everything runs client-side — data is stored in `localStorage`, export CSV/JSON
when ready. This is a separate site from your other coders — set it up as its own GitHub
repo with its own Pages URL.

## How the numbers work

Each story panel is laid out top to bottom as:

1. **Story Enjoyment** and **Character Similarity** (1–5)
2. **Totals summary** (auto-calculated, shown before the detail sections below):
   - **Total Number of Reasons** = Total Positive Reasons + Total Negative Reasons
   - **Total Relevant Reasons** = (Positive Plot + Positive Character) + (Negative Plot + Negative Character)
   - **Total Irrelevant Reasons** = Total − Relevant
3. **Positive Reasons** and **Negative Reasons** sections, where you enter:
   - **Total Number of Reasons** for that group — you enter this directly (the total count of reasons the child gave, relevant or not)
   - **Plot Reasons** and **Character Reasons** checklists — check off which specific reason types applied; the count is the number of boxes checked
   - **Relevant Reasons** (= Plot + Character for that group) and **Irrelevant Reasons** (= Total − Relevant for that group) — both shown automatically

## Reason type checklists — easy to expand

- **Plot Reasons**: **Favourite event 1**, **Favourite event 2**, **Favourite event 3**
- **Character Reasons**: **Favourite color**, **Favourite outfit**, **Favourite food**,
  **Hair color**, **Eye color**

To add more reason types to either list, open `index.html`, find these two lines near the
top of the `<script>` section, and add items:

```js
const PLOT_REASON_TYPES = ["Favourite event 1", "Favourite event 2", "Favourite event 3"];
const CHARACTER_REASON_TYPES = ["Favourite color", "Favourite outfit", "Favourite food", "Hair color", "Eye color"];
```

New items automatically show up in the checklist and in CSV export — no other changes needed.

## What it captures

- **Participant ID**, **Control ID** (linked to the participant, not a separate record)
- For **each** story (High Preference, Low Preference/Control):
  - **Positive Reasons**: total count (manual), Plot Reasons checklist, Character Reasons checklist, Relevant Reasons (auto)
  - **Negative Reasons**: same structure
  - **Total Number of Reasons** for the story (auto)
  - **Story Enjoyment** (1–5)
  - **Character Similarity** (1–5) — assumed to use the same 1–5 scale as enjoyment; let me know if you'd like a different range

## Publishing to GitHub Pages

1. Create a new GitHub repo (e.g. `reasoning-coder`).
2. Add `index.html` to it.
3. In the repo settings, enable **GitHub Pages** for the `main` branch (root folder).
4. Your tool will be live at `https://<your-username>.github.io/<repo-name>/`

## Export format

CSV export is in **wide format**, matching your original spreadsheet template — one row
per participant, with separate columns for each metric per story (high preference / low
preference), including the summary numbers (total reasons, relevant reasons, plot/character
counts) plus a detailed Yes/No column for every individual checklist item, for full
traceability back to what was actually checked.

## Notes

- Data lives only in the browser tied to the exact URL you use — always enter data through
  your one published GitHub Pages link, not downloaded local copies of the file.
- The "Participants saved in this browser" panel shows exactly which participant IDs are
  currently stored, so you can verify nothing's missing before exporting.
