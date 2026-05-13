# Portfolio Rebuild Plan

## Recommendation

Rebuild the portfolio inside the same GitHub Pages repository using Quarto.

Do not continue extending the existing Beautiful Jekyll theme. The current Jekyll site has useful project assets and some relevant portfolio material, but the structure, visual system, and content model are too dated for a strong data analysis / machine learning portfolio.

## Pre-Implementation Decisions

Resolve these decisions before writing the first production `.qmd` page.

### Phase 0 Deployment Proof

Before content migration or design work, prove that Quarto deployment works.

Status: completed. The `gh-pages` branch is serving the Quarto "Hello" deployment proof at `https://zekariasm.github.io`.

Phase 0 requirements:

- Scaffold a one-page Quarto site.
- Run `quarto publish gh-pages`.
- Verify the site serves at `https://zekariasm.github.io`.
- Confirm GitHub Pages is configured to serve from `gh-pages` / root.
- Confirm rendered output includes `.nojekyll`.

Do not proceed to full Phase 1 implementation until this works.

### Deployment

Use `quarto publish gh-pages` as the preferred deployment path.

Recommended setup:

- Source files live on the working rebuild branch.
- Rendered site is published to the `gh-pages` branch.
- GitHub Pages serves the rendered static output from `gh-pages`.
- Quarto handles the static output and `.nojekyll` behavior.

Do not render the site into `docs/` on the main branch unless there is a strong reason. Keeping source and rendered output mixed in one branch will create noisy diffs and make the repo harder to review.

GitHub Actions can be added later if automated publishing becomes important, but it is not required for the first rebuild.

### Cutover Strategy

Build the Quarto site on the current `portfolio-upgrade` branch while the existing Jekyll site remains untouched on `main`.

Cut over only after:

- The Quarto site renders locally.
- The rendered site publishes successfully.
- Navigation works.
- Old URLs are handled.
- Mobile layout is acceptable.
- The MVP pages have real content.

At final cutover, remove or archive the old Jekyll-specific files only after the Quarto site is verified.

Likely remove/archive:

- `_config.yml`
- `_layouts/`
- `_includes/`
- `_posts/`
- `Portfolio.md`
- `DataAnalysis.md`
- `spatial.md`
- `visualization.md`
- `index.md`
- `2index.html`
- `4504.html`
- `xxxindex.html`
- `xxxindex.md`
- `404.html`
- `blog/`
- `css/`
- `feed.xml`

Likely keep:

- `img/` until assets are fully migrated
- `files/STH_Kenya.pdf`
- `favicon.ico`
- `favicon.ico.png`, if reused
- `LICENSE`
- `README.md`, rewritten for the new Quarto site

### MVP Launch Scope

Launch with a small number of complete pages. Do not publish empty project stubs or "coming soon" pages.

MVP pages:

- Home
- Projects index
- Atlanta Arts and Entertainment Clustering case study
- Spatial Health Risk Kenya case study
- About
- Resume
- Contact

Post-MVP projects should be added only when each one has enough evidence to stand on its own.

### Python Execution Environment

Use Quarto with the Jupyter engine for Python-based reports and dashboards.

Add a pinned Python dependency file before rendering analytical content:

- `requirements.txt` for a simple Python setup, or
- `environment.yml` if conda-specific geospatial dependencies are needed.

Enable Quarto execution freezing from the start:

```yaml
execute:
  freeze: auto
```

This prevents every site render from rerunning notebooks and reduces breakage from changing APIs, package versions, and remote data sources.

### Existing URL Strategy

Preserve important existing URLs with Quarto aliases or lightweight redirect pages.

Likely old URLs to preserve:

- `/Portfolio`
- `/Portfolio.html`
- `/2020-12-29-battle/`
- `/spatial`
- `/spatial.html`
- `/visualization`
- `/visualization.html`
- `/DataAnalysis`
- `/DataAnalysis.html`

The Atlanta project should become the destination for the current `Portfolio` and blog-post versions of the Battle of the Neighborhoods content.

### Atlanta Data Source Strategy

The Atlanta project depends on historical Foursquare/API data. Before rewriting the case study, choose one path:

- Preserve the original data/results as a historical 2020 analysis and clearly label the data vintage.
- Recreate the project with a modern open source data source such as OpenStreetMap Overpass or Overture Maps.

For the MVP, prefer preserving the historical analysis with a clear caveat. Rebuilding the data pipeline with a new source is valuable, but it is a separate project-sized effort.

### Theme And Brand Defaults

Use a clean, conservative Quarto visual system for the first version.

Initial defaults:

- Theme: `cosmo`
- Accent color: `#2563eb`
- Typography: system sans stack or Inter if added cleanly
- Tone: professional, analytical, concise
- Custom domain: none; keep `https://zekariasm.github.io`

Hero headline draft:

```text
Zekarias M. — Data analyst focused on Python, SQL, dashboards, geospatial analysis, and machine learning.
```

These can be refined, but the first build should avoid spending time on heavy visual customization.

### Resume Strategy

Use one resume source if possible.

Preferred approach:

- Create `resume.qmd` as the canonical resume source.
- Render it as an HTML resume page.
- Add a PDF export or linked PDF once the resume content is ready.

Do not maintain unrelated resume text in multiple places.

### Contact Strategy

Keep `contact.qmd` only if it has complete contact information.

Minimum content:

- Email
- GitHub
- LinkedIn
- Optional calendar link

If contact content is too thin, merge it into About and the site footer instead of keeping a weak standalone page.

### Pre-Flight Asset Inventory

Gather these before production page work:

- LinkedIn profile URL
- Current resume content
- Profile photo, preferably square and at least 400 by 400 pixels
- Preferred email address for public contact
- Optional calendar link
- Favicon / Open Graph image source, even if it is a simple initials graphic
- Confirmed hero headline and short bio

### Local Development Workflow

Use these commands during the rebuild:

```bash
quarto preview
quarto render
quarto publish gh-pages
```

Run `quarto preview` for local iteration, `quarto render` before reviewing generated output, and `quarto publish gh-pages` only after the local render is clean.

## Current Repo Assessment

The current repo is a small GitHub Pages site built with Jekyll, Markdown pages, Liquid layouts, Bootstrap 3-era CSS, and a Beautiful Jekyll-derived theme. It contains one substantial project writeup, several thin topic pages, image assets, a PDF, and embedded mapping content.

### Useful Parts To Preserve

- The GitHub Pages repo and public portfolio URL.
- Existing project assets under `img/por/`, especially geospatial maps, screenshots, and clustering visuals.
- The Atlanta arts and entertainment neighborhood clustering project.
- The spatial analysis PDF in `files/STH_Kenya.pdf`.
- The economics, geospatial, and public-policy analysis angle.
- GitHub identity and public portfolio history.

### Problems With The Current Implementation

- The homepage has almost no content and does not quickly communicate target roles, skills, or proof.
- Navigation is organized around old topic buckets instead of recruiter-friendly sections.
- The site reads like a course archive rather than a professional portfolio.
- The current theme is visually dated and constrains the site structure.
- There is no reusable project or case-study template.
- Project evidence is mostly screenshots and narrative, with limited links to code, notebooks, dashboards, or reproducible artifacts.
- The repo has no local build dependency file such as `Gemfile`.
- The layout references JavaScript files that are not present in the repo.
- Some links and metadata are stale or likely broken.
- Current content needs rewriting for clarity, grammar, credibility, and business impact.

## Target Outcome

Build a credible data analysis / machine learning portfolio for:

- Data analyst roles
- Business analyst roles
- Junior data scientist roles
- ML-oriented analyst roles
- Freelance or consulting analytics clients

The site should answer these questions quickly:

- Who is Zekarias?
- What roles is he targeting?
- What technical skills can he prove?
- What projects demonstrate those skills?
- What business or research problems has he solved?
- Where can a recruiter see code, dashboards, notebooks, or reports?

## Chosen Stack

### Primary Stack: Quarto

Use Quarto as the new build system inside the same repository.

Reasons:

- Strong fit for data analysis and ML portfolios.
- Supports Markdown, executable notebooks, code blocks, citations, figures, tables, and reports.
- Works well with Python and Jupyter workflows.
- Publishes clean static output suitable for GitHub Pages.
- Makes case studies feel like professional analytical reports instead of generic blog posts.
- Easier to maintain than a custom frontend-heavy stack.

### Why Not Continue Current Jekyll

Jekyll can work for simple blogs, but this repo's current Jekyll setup is not a strong foundation. Keeping it would require theme cleanup, layout redesign, navigation restructuring, asset fixes, and content migration while still leaving a less data-native publishing workflow.

### Why Not Astro First

Astro is a good option for a polished custom frontend, but it is more engineering work and less naturally aligned with notebook-driven analytics. It is better if the primary goal becomes a highly customized web experience rather than a data portfolio.

## Proposed Site Structure

```text
/
  _quarto.yml
  requirements.txt
  index.qmd
  about.qmd
  resume.qmd
  contact.qmd
  projects/
    index.qmd
    atlanta-arts-clustering.qmd
    spatial-health-risk-kenya.qmd
  assets/
    images/
    dashboards/
    pdfs/
    data-samples/
```

## Proposed Navigation

- Home
- Projects
- Resume
- About
- Contact

Remove the current primary navigation labels:

- Blog
- Data Analysis
- Portfolio
- Visualization
- Spatial Analysis

Those can become project filters or skill tags instead of top-level navigation.

Do not add a Writing or Blog section at launch unless it has real posts. Empty sections hurt credibility.

## Homepage Plan

The homepage should contain:

- A direct headline positioning Zekarias as a data analyst / ML-oriented analyst.
- A short value proposition focused on Python, SQL, dashboards, statistics, ML, and geospatial analysis.
- Three to five featured project cards.
- A compact skills section grouped by evidence.
- Links to GitHub, resume, LinkedIn, and email.

Suggested homepage sections:

```text
Hero
Featured Projects
Technical Skills
About Snapshot
Contact
```

Avoid duplicating the same skills and artifacts across too many pages. Skills should appear on the homepage and About page, tied to project evidence. The Projects page should be the main source of truth for artifacts.

## Project Case Study Template

Each project should use a consistent case-study structure:

```text
Title
Outcome
Role / Tools / Timeline
Business or Research Question
Why It Matters
Data Sources
Methods
Key Findings
Artifacts
  - GitHub repo
  - Notebook or report
  - Dashboard
  - Dataset or data dictionary, when shareable
Technical Highlights
Limitations
Reproducibility / How To Run
Next Steps
```

For machine learning projects, add:

```text
Target Variable
Feature Engineering
Train/Test Split
Baseline Model
Model Comparison
Evaluation Metrics
Error Analysis
Deployment or Reproducibility Notes
```

## Content To Preserve And Rewrite

### Atlanta Arts And Entertainment Clustering

Preserve:

- Existing maps and clustering images.
- Existing Folium HTML maps if they render correctly.
- The geospatial analysis premise.
- Use of Python, pandas, Folium, Foursquare/API data, and K-means clustering.

Rewrite:

- Make the first section outcome-oriented.
- Reduce generic background about Atlanta.
- Fix grammar and terminology.
- Add a concise methods table.
- Add technical links if source code exists or can be recreated.
- Add limitations around Foursquare/API coverage and clustering interpretation.
- Add business recommendations.

Asset migration rules:

- Move project assets to `assets/images/atlanta/`.
- Replace code screenshots with real code blocks where practical.
- Replace table screenshots with rendered tables where practical.
- Keep map images and interactive Folium HTML maps if they improve the case study.
- Embed `atl_map1.html` and `atl_map2.html` as iframes if they still render correctly.

### Spatial Health Risk Kenya

Preserve:

- `files/STH_Kenya.pdf`
- ArcGIS / spatial modeling angle

Rewrite:

- Convert from a single PDF link into a real project page.
- Add summary, methods, map previews, tools, findings, and artifact links.

### Visualization / ArcGIS COVID Map

Preserve only if it can be framed as a real dashboard or mapping artifact.

Rewrite:

- Add context, audience, data source, decisions, and interpretation.
- Avoid leaving it as a lone iframe.

## New Project Coverage Needed

To be credible for analyst and junior data science roles, the portfolio should include evidence across these areas:

- Python: pandas cleaning, EDA, visualization, reproducible notebook.
- SQL: joins, CTEs, window functions, aggregation, business metrics.
- Excel: pivot tables, formulas, scenario analysis, dashboard workbook.
- Power BI or Tableau: dashboard with measures, filters, and business interpretation.
- Statistics: regression, A/B test, confidence intervals, hypothesis testing.
- Machine learning: supervised model with proper baseline, metrics, and error analysis.
- Geospatial analysis: GeoPandas, Folium, ArcGIS, spatial joins, choropleth or clustering.
- Data storytelling: executive summary, recommendations, limitations, and next steps.

## Prioritized Implementation Roadmap

### Phase 0: Deployment Proof

- Scaffold a one-page Quarto site.
- Publish it to `gh-pages`.
- Verify `https://zekariasm.github.io` serves the Quarto output.
- Confirm GitHub Pages source is `gh-pages` / root.
- Confirm `.nojekyll` exists in rendered output.
- Stop and fix deployment if this does not work.

### Phase 1: Foundation

- Add Quarto config.
- Add deployment target using `quarto publish gh-pages`.
- Add `.nojekyll` to rendered output through the Quarto publishing flow.
- Add `requirements.txt` or `environment.yml`.
- Enable `execute.freeze: auto`.
- Define global navigation.
- Create homepage, projects index, about, resume, and contact pages.
- Set site metadata, description, Open Graph image, favicon, and sitemap settings.
- Add analytics only if there is a clear preference for a privacy-respecting tool.
- Add old URL aliases or redirect pages.
- Move preserved assets into a cleaner `assets/` structure.
- Add Quarto project listings only after real case-study pages exist. Avoid empty listing warnings and empty project cards.

### Phase 2: Existing Content Migration

- Convert the Atlanta project into a polished case study. Initial Quarto case-study page created; final credibility upgrade still requires source notebook or recreated code.
- Convert the Kenya spatial analysis PDF into a project page.
- Decide whether to preserve, rewrite, or remove the ArcGIS visualization page.
- Remove or archive duplicate old files after the new site is working.

### Phase 3: Portfolio Depth

- Add one SQL business analysis project.
- Add one dashboard project using Power BI or Tableau.
- Add one Excel analysis project.
- Add one machine learning project with clear evaluation.
- Add one statistics-focused project or integrate statistical testing into a project.

This phase is larger than the site rebuild itself. It represents several weeks of real analytical work and should be treated as the main portfolio-building phase, not a quick cleanup phase.

### Phase 4: Credibility Polish

- Add project cards with tools, methods, artifacts, and outcomes.
- Add GitHub links and downloadable reports.
- Check mobile layout.
- Run a broken-link check.
- Verify GitHub Pages deployment.

## Risks And Tradeoffs

- Quarto is less flexible than Astro for highly custom interactive frontend design.
- Rebuilding will temporarily require careful handling of old URLs and assets.
- Some existing project content may need source notebooks or recreated code to become credible.
- The biggest hiring risk is thin proof, not the site stack. The rebuild should prioritize artifacts that prove skill.
- Old Jekyll files should not be deleted until the Quarto site renders and deploys correctly.
- Re-executing notebooks during every render can break the site when APIs, data sources, or package versions change. Use `freeze: auto`.
- Publishing empty project stubs will make the portfolio look weaker. Only publish complete projects.
- The first technical milestone should be a working Quarto deployment, before deep content migration.

## Final Decision

Proceed with a same-repo Quarto rebuild.

The goal is not just a visual refresh. The goal is to turn the portfolio into a structured evidence system for data analysis, business analysis, junior data science, and ML-oriented roles.
