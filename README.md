# Figure Tools

A small, no-dependency, multi-page site for building publication-style scientific figures by hand. Everything runs in the browser.

- **`index.html`** — home page linking to all tools.
- **`timeline.html`** — study/trial timeline diagrams.
- **`domains.html`** — protein domain / structure organization maps, with a manual plot width/height (cm/mm/in) and the 40-color hex palette (displays correctly in Adobe Illustrator).
- **`plots.html`** — Violin / Density / Line plots (tabs switch chart type):
  - CSV/TSV paste or CSV/Excel upload, one-click sample data.
  - Per-column "Show in plot" checkbox to include/exclude variables.
  - Explicit **Start / End / Tick count** for each axis, auto-filled from your data when you load it and freely editable, plus separate axis-line-to-label spacing (px) for X and Y.
  - Fully independent **font family, style, size and color** for axis tick numbers, axis titles, and legend/category labels.
  - Legend **position** (4 corners) and layout (stacked or row) for the series legend, and a separate positionable legend for the violin plot's 25–75% / 1.5×IQR / Mean key (editable text, stacked or 3-across).
  - Region annotations on line plots with an auto-built legend, and a **Renumber residues** offset field to shift X values (e.g. renumber a fragment to start at a different residue number).
  - Export as SVG, or as a **vector PDF** (via svg2pdf.js) that opens as editable paths/text in Adobe Illustrator — not a flattened image.
- **`multipanel.html`** — compose multiple datasets into one page:
  - **Violin + Density Grid**: upload multiple CSV/Excel files (one file = one column). Choose the number of columns, whether each dataset shows violin only / density only / both, and the panel arrangement (violin above/below density, or side by side); set column and row gaps; size panels manually (per column width, per row height) or auto-fit to a page. Every dataset keeps the same per-group show/hide + label + color controls as Analysis Plots. A "Bulk Apply" panel lets you set the axis label, tick start/end/step (with a whole-numbers-only option), tick-label distance, and font size/color for a chosen subset of datasets at once (e.g. label datasets 1 and 3 "RMSD (Å)" and 2 and 4 "Rg (Å)").
  - **Line Stack**: add any number of line plots, stacked vertically or arranged in a row. Each plot keeps its own data, per-series show/hide/color/style, region annotations, residue-renumbering offset, and explicit X/Y tick start/end/step (whole-numbers-only option) — editable individually, or set for a chosen subset of plots at once via "Bulk Apply to Selected Plots" (e.g. renumber plots 1–2 starting at 20 and plots 3–4 starting at 29) and "Bulk Add Region" (add one domain/region to just the plots you pick). Each plot's legend can be shown or hidden independently.
  - Both export to SVG or vector PDF.

- **`shared.js`** — kept for reference only (palette, CSV/Excel parsing, stats, tick generation, font-control UI, SVG/PDF export helpers). `plots.html` and `multipanel.html` now embed this code directly, so **no page needs `shared.js` present to work** — each HTML file is fully self-contained and safe to open or share on its own.

- **`dccm.html`** — dynamic cross-correlation matrix (DCCM) heatmaps from Excel/CSV matrix files (first row/column = index, rest = the correlation matrix):
  - **Two-File Comparison**: upload two matrices, renumber the residue axis (row/col 1 → your chosen starting residue), pick which file is subtracted from which, set a cutoff so only |value| ≥ cutoff is shown in the difference plot, and choose the positive/negative colors from the 40-color palette. All three panels (File A, File B, Difference) sit in one row sized to fit a page. Download the difference matrix as CSV.
  - **Multi-File Grid**: upload 6 (or more) files; they fill rows in upload order (set how many per row), and within each row the first file is the baseline — every other file in that row automatically gets its own difference-vs-baseline panel, laid out in a second grid below the raw one on the same page, with independent plots-per-row and gap control. Download every difference matrix as CSV in one click.
  - Shared style controls: several diverging heatmap colormaps (or pick your own 3 anchor colors), tick step and tick-label distance, and separate font controls for tick numbers and panel titles.
  - Exports to SVG or vector PDF.

## Run it locally
Open `index.html` in any browser. Excel parsing, PDF export, and the sample-data buttons need an internet connection (they load small libraries from a CDN); everything else works offline.

## Host it on GitHub Pages
1. Create a new repository on GitHub (e.g. `figure-tools`).
2. Add all the files above to the repo — via the GitHub web UI ("Add file → Upload files") or:
   ```
   git init
   git add index.html timeline.html domains.html plots.html multipanel.html dccm.html README.md
   git commit -m "Add multi-panel layout tool"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```
3. In the repo, go to **Settings → Pages**, set Source to "Deploy from a branch", branch `main`, folder `/ (root)`, then Save.
4. Your site will be live at: `https://<your-username>.github.io/<your-repo>/`

## Data format
- **Violin / Density**: each column is one group's sample values; first row = group names.
- **Line**: column 1 = X values; each remaining column is one line series, named by its header.
- **Multi-Panel Grid**: one file per grid column, each file in the Violin/Density format above.

## Editing further
Each HTML file is self-contained aside from the shared `shared.js`, so you can tweak one tool without affecting the others.
