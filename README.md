# Sarah Hancock's Lab Tools

A suite of interactive calculators and data tools for everyday wet-lab work. Everything runs in the browser: there is nothing to install, no server, and no data leaves your machine.

**Live site:** `https://<username>.github.io/<repo-name>/`

## Tools

| Tool | What it does | Export |
| --- | --- | --- |
| **BCA Protein Assay** | Standard curve fitting (linear, 2nd-order polynomial, 3PL or 4PL), replicate QC with a CV% flag threshold, and sample concentration calculation with dilution factor. Plate data and labels can be pasted straight from Excel. | CSV |
| **Western / Laemmli Prep** | Sample, RIPA and Laemmli buffer volumes (6×, 4× or 2×) for a target protein load per well, with Criterion 18- and 26-well gel layouts. BCA concentrations can be pasted in from the BCA export or Excel. | CSV |
| **Cell Culture Plating** | Seeding density calculations for dishes, flasks and 6- to 96-well plates, serial dilution schemes, and transfection plate layouts. | CSV |
| **qPCR ΔΔCt** | ΔΔCt analysis with multi-reference-gene geometric mean normalisation, standard or custom PCR efficiency, and group comparisons as fold change or log₂ fold change. | CSV |
| **IC50 Calculator** | 4PL dose-response fitting for one or two cell lines, with free or fixed Hill slope, top and bottom, an F-test between curves, and bootstrap 95% confidence intervals. | Markdown, PNG, SVG |
| **Stock & Dilution** | Stock preparation, working dilutions, a DMSO % checker for final solutions, and a compound library that can be imported from CSV. | Markdown |

## Using the site

Open the site and pick a tool from the sidebar. Each tool loads the first time you select it and keeps its state while you switch between tools.

Nothing is saved between visits. Inputs, results and the compound library in Stock & Dilution live in memory only and are cleared when the page is reloaded or closed, so export anything you want to keep.

## Running locally

The site is plain HTML, CSS and JavaScript with no build step. Either open `index.html` directly in a browser, or serve the folder:

```bash
python3 -m http.server 8000
```

then go to `http://localhost:8000`.

## Project structure

```
.
├── index.html            # Shell: header, sidebar and tool loader
├── tools/
│   ├── bca.html          # BCA Protein Assay
│   ├── western.html      # Western / Laemmli Prep
│   ├── cell_culture.html # Cell Culture Plating
│   ├── qpcr.html         # qPCR ΔΔCt
│   ├── ic50.html         # IC50 Calculator
│   └── stocks.html       # Stock & Dilution
├── .nojekyll             # Tells GitHub Pages to serve files as-is
└── robots.txt
```

Each tool is a single self-contained HTML file that `index.html` loads in an iframe. The only external resource is the IBM Plex font family from Google Fonts; the tools still work offline, falling back to system fonts.

## Deploying to GitHub Pages

1. Push the contents of this folder to the root of the repository, including the hidden `.nojekyll` file.
2. In the repository, go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, then select `main` and `/ (root)`.
4. The site is published at `https://<username>.github.io/<repo-name>/` after a minute or so.

All links are relative, so the site works from a project sub-path without any configuration.

## Adding a tool

1. Add a self-contained HTML file to `tools/`.
2. In `index.html`, add three things, following the existing entries: a `nav-item` in the sidebar with `data-tool="tools/<file>.html"`, a card on the welcome screen, and an `<iframe class="tool-frame">` with a matching `id="frame-tools/<file>.html"` and `data-src`.

## Search engines

Every page carries a `noindex, nofollow` meta tag, so the site is kept out of search results. Remove that tag from each page's `<head>` if you want it indexed. `robots.txt` is kept for hosts that serve the site from a domain root; GitHub Pages ignores it on project sites.

## Disclaimer

These tools are provided for convenience. Check calculations against your own protocols before relying on them for experiments.

## Author

Sarah Hancock
