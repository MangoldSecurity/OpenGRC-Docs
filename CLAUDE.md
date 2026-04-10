# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is the **documentation repository** for OpenGRC, a Laravel/Filament-based Governance, Risk, and Compliance (GRC) web application. Documentation is built with MkDocs (Material theme) and deployed to https://docs.opengrc.com.

**Important**: The OpenGRC application codebase is at `/var/www/html/sites/OpenGRC-Commercial`. Reference it for writing accurate documentation but do NOT edit it from this repo context.

## Documentation Build Commands

```bash
# Serve documentation locally (default port 8000)
mkdocs serve

# Build static documentation site
mkdocs build

# Deploy to GitHub Pages (if configured)
mkdocs gh-deploy
```

Always run `mkdocs build` after changes to verify no errors.

## Project Structure

```
docs/
  index.md              # Landing page
  features/             # Community feature documentation
  enterprise/           # Enterprise-only feature documentation
  foundations/           # Core GRC concepts
  settings/             # Configuration pages
  sso/                  # Single Sign-On guides
  data-manager/         # Import/export guides
  img/                  # Images and screenshots
    enterprise/         # Enterprise feature screenshots
  stylesheets/
    extra.css           # Custom CSS (tables, screenshots, enterprise admonition)
mkdocs.yml              # MkDocs configuration (Material theme)
```

## Adding New Documentation Pages

1. Create the `.md` file in the appropriate directory (`docs/features/` or `docs/enterprise/`)
2. Add the page to the `nav:` section in `mkdocs.yml`
3. Run `mkdocs build` to verify

## Enterprise Features

Enterprise-only features go under `docs/enterprise/` and the "Enterprise Features" nav section in `mkdocs.yml`.

Every enterprise feature page MUST include the enterprise admonition badge at the top, immediately after the H1 title:

```markdown
# Feature Name

!!! enterprise "Enterprise Feature"
    The Feature Name module is available exclusively in OpenGRC Enterprise. [Learn more about Enterprise](https://opengrc.com).
```

This renders a purple-bordered admonition with a shield-check icon. The styling is defined in `extra.css` as a custom admonition type.

Community features go under `docs/features/` and do NOT get the enterprise badge.

## Documentation Style

### Page Structure

Follow this structure for feature documentation pages:

1. **H1 title** with feature name
2. **Enterprise badge** (enterprise features only)
3. **Introductory paragraph** describing what the feature does
4. **Hero screenshot** showing the main view
5. **Overview** section with bullet list of capabilities
6. **Feature sections** with screenshots, attribute tables, and step-by-step instructions
7. **Configuration** section if applicable
8. **Best Practices** section
9. **Permissions** section

### Formatting Conventions

- Bold for UI elements: `**Settings > AI**`, `**New Project**`
- Bold for field names in tables: `**Name**`, `**Status**`
- Inline code for technical values: `` `question` ``, `` `true` ``
- Use Mermaid diagrams for process flows (the `pymdownx.superfences` extension is configured for this)
- Use admonitions for warnings and notes: `!!! warning "Title"`

### Tables

Tables are styled globally via `extra.css` with:
- Blue header row (site primary color `#0f5a7a`)
- Compact font size (0.75rem) and tight padding
- Full width layout

No special markup needed -- standard markdown tables get these styles automatically.

## Screenshots with Playwright MCP

Use the Playwright MCP tools to capture screenshots from the running OpenGRC application.

### Authentication

Bypass login by appending `?authid=1` to any URL:
```
http://commercial.test/app/survey-processor?authid=1
```
Only needed on the first navigation; the session persists after that.

### Screenshot Workflow

1. **Navigate** to the page with `browser_navigate`
2. **Take a snapshot** with `browser_snapshot` to get element refs
3. **Capture cropped screenshots** using `browser_run_code` with clip regions

### Cropping Strategy

NEVER take full-page screenshots -- they include the sidebar, empty whitespace, and debug bars. Instead, use JavaScript via `browser_run_code` to clip to just the content:

```javascript
async (page) => {
  await page.goto('http://commercial.test/app/some-page');
  await page.waitForLoadState('networkidle');

  // Get the main content area bounds
  const main = page.getByRole('main');
  const mainBox = await main.boundingBox();

  // Find a landmark element at the bottom of the visible content
  const bottomElement = page.getByText('Some text at the bottom');
  const bottomBox = await bottomElement.boundingBox();
  const contentBottom = bottomBox.y + bottomBox.height + 30; // 30px padding

  await page.screenshot({
    path: 'feature-section-name.png',
    type: 'png',
    scale: 'css',
    clip: {
      x: mainBox.x,
      y: mainBox.y,
      width: mainBox.width,
      height: contentBottom - mainBox.y
    }
  });
  return 'Done';
}
```

Key principles:
- Use `mainBox.x` and `mainBox.y` as the top-left origin to exclude the sidebar
- Find a bottom landmark element (last table row, last button, pagination text) to determine content height
- Add ~20-30px padding below the bottom landmark
- For section-specific crops, use the section heading as the top origin instead of `mainBox.y`
- Multiple screenshots can be taken in a single `browser_run_code` call

### Saving Screenshots

- Save screenshots to `docs/img/enterprise/` for enterprise features
- Use descriptive filenames: `feature-section.png` (e.g., `surveyor-hero.png`, `remediation-kanban.png`)
- Reference in markdown with relative paths: `![Alt text](../img/enterprise/filename.png)`

### Tab/View Navigation

For pages with multiple tabs (Summary, Board, List), use `browser_click` or include tab clicks in the `browser_run_code` script:

```javascript
await page.getByRole('button', { name: 'Board' }).click();
await page.waitForTimeout(1500); // Wait for tab content to load
```

## Markdown Extensions

The following extensions are enabled in `mkdocs.yml`:

- `admonition` -- callout boxes (`!!! note`, `!!! warning`, `!!! enterprise`)
- `pymdownx.details` -- collapsible admonitions (`??? note`)
- `attr_list` -- add HTML attributes to elements
- `pymdownx.superfences` -- fenced code blocks with Mermaid diagram support

## OpenGRC Application Context

When writing documentation, reference these key OpenGRC concepts:

- **Programs** - Organizational groupings for compliance initiatives
- **Standards** - Compliance frameworks (NIST, ISO, CMMC, etc.)
- **Controls** - Individual security requirements within standards
- **Implementations** - How controls are actually implemented
- **Audits** - Assessment processes with audit items
- **Risks** - Risk management entities

The application is built with Laravel 12 and Filament 4, uses Sanctum for API authentication, and supports MySQL/MariaDB/SQLite databases. Enterprise features are implemented as Laravel modules under `Modules/` in the commercial codebase.
