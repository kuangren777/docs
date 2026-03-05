# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Mintlify documentation site. Mintlify transforms MDX files into documentation sites with configuration in `docs.json`.

## Essential Commands

### Development
```bash
# Install Mintlify CLI (first time only)
npm i -g mint

# Start local preview server at http://localhost:3000
mint dev

# Update CLI to latest version
mint update
```

### Validation
```bash
# Check for broken internal links
mint broken-links

# Check accessibility issues
mint a11y

# Validate documentation builds
mint validate
```

### File Operations
```bash
# Rename/move files and update all references automatically
mint rename <old-path> <new-path>
```

## Architecture

### Core Files
- **`docs.json`**: Site configuration - navigation structure, theme, colors, tabs, API specs
- **`*.mdx`**: Documentation pages with YAML frontmatter (title, description required)
- **`api-reference/openapi.json`**: OpenAPI specification for auto-generated API docs
- **`.agents/skills/mintlify/SKILL.md`**: Mintlify best practices and component reference

### Navigation Structure
The site uses a **tabs-based** navigation pattern in `docs.json`:
- **Guides tab**: Getting started, customization, writing content, AI tools
- **API reference tab**: API documentation and endpoint examples

Pages must be added to `docs.json` navigation to appear in the sidebar.

### Content Organization
```
/
├── docs.json              # Site config
├── index.mdx              # Homepage
├── quickstart.mdx         # Getting started
├── development.mdx        # Local dev guide
├── essentials/            # Core documentation features
├── ai-tools/              # AI tool integration guides
├── api-reference/         # API documentation
│   ├── introduction.mdx
│   ├── openapi.json       # OpenAPI spec
│   └── endpoint/          # API endpoint examples
├── snippets/              # Reusable MDX components
├── images/                # Static assets
└── logo/                  # Brand assets
```

## Writing Documentation

### Page Requirements
Every MDX file must have frontmatter with at minimum:
```yaml
---
title: "Page title"
description: "SEO description"
---
```

### Internal Links
- Use root-relative paths without file extensions: `/quickstart` not `./quickstart.mdx`
- Never use relative paths (`../`) or absolute URLs for internal pages

### Style Guidelines
- Active voice, second person ("you")
- Sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths
- One idea per sentence

### Common Components
Refer to `.agents/skills/mintlify/SKILL.md` for full component reference. Key components:
- `<Card>` - Navigation cards
- `<Accordion>` - Collapsible content
- `<Tabs>` - Multiple options
- `<CodeGroup>` - Multi-language code examples
- `<Note>`, `<Tip>`, `<Warning>` - Callouts

## Workflow for Changes

1. **Read `docs.json`** to understand site structure
2. **Search existing docs** before creating new pages
3. **Read similar pages** to match style
4. **Create/edit MDX files** with proper frontmatter
5. **Update `docs.json` navigation** if adding new pages
6. **Run `mint broken-links`** to validate
7. **Preview with `mint dev`** before committing

## Deployment

Changes deploy automatically when pushed to the main branch via Mintlify's GitHub app integration.

## AI Tool Integration

This project has a Mintlify skill installed at `.agents/skills/mintlify/`. Always consult this skill file for:
- Component syntax and usage
- Configuration options
- Best practices
- Latest Mintlify features

Install the skill in other projects with:
```bash
npx skills add https://mintlify.com/docs
```

## Important Notes

- **Never use `mint.json`** - it's deprecated. Only use `docs.json`
- All code blocks must have language tags
- Hidden pages (not in navigation) are still accessible by URL
- Use `.mintignore` to exclude files from processing
