# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hugo-based multilingual book translation project for "Building Blocks of Liberty" by Walter Block. The repository hosts both the original English text and Chinese translation (Traditional Chinese, zh-tw), published under Creative Commons Attribution License.

You are an expert of Libertarianism, using an consistant knowledge of the Mises like theory to translate the content.

## Development Commands

### Local Development Server
```bash
hugo server --gc --minify --cleanDestinationDir --gc -t hugo-book
```

### Build for Production
```bash
hugo --gc --minify --cleanDestinationDir --gc -t hugo-book
```

The build output goes to the `resources/` directory (configured via `publishDir` in config.yaml).

## Architecture

### Hugo Configuration
- **config.yaml**: Main configuration file
  - baseURL points to GitHub Pages deployment
  - Default language: Chinese (zh)
  - Bilingual support: Chinese (zh) and English (en)
  - Theme: hugo-book (included as git submodule)
  - publishDir set to `resources/` instead of default `public/`

### Content Organization
All content is in `content/docs/` with bilingual files using language suffixes:
- `.en.md` for English content
- `.zh.md` for Chinese translations

Content is organized into three main parts:
1. **part-1-economics/**: Economic theory and applications
2. **part-2-human-rights/**: Human rights and libertarian philosophy
3. **part-3-language/**: Language usage and political terminology

Each part has:
- `_index.en.md` and `_index.zh.md` for section pages
- Individual chapter files with naming pattern: `part-{number}-{chapter}-{title}.{lang}.md`

Top-level documents (acknowledgements, foreword, introduction, bibliography) are directly in `content/docs/` with numbered prefixes (01-, 02-, etc.) for ordering.

### Content Frontmatter
Each content file uses YAML frontmatter with:
- `title`: The chapter/section title
- `weight`: Controls ordering in navigation (lower numbers appear first)
- `bookCollapseSection`: For section index pages, controls whether subsections are collapsed by default

### Translation Status
- 30 English content files (.en.md)
- 10 Chinese translations (.zh.md) completed
- Translation is ongoing, with more English chapters than Chinese

## Deployment

### GitHub Actions
Automated deployment via `.github/workflows/deploy.yml`:
- Triggers on push to `master` branch
- Uses latest Hugo Extended version
- Builds site with the same command as local development
- Deploys to GitHub Pages (gh-pages branch)
- Requires `PUSH_REPO_TOKEN` secret for deployment

### Submodules
The hugo-book theme is included as a git submodule. When checking out:
```bash
git submodule update --init --recursive
```

## Theme Customization

The hugo-book theme configuration in config.yaml params:
- Dark theme enabled by default (`BookTheme: dark`)
- Search enabled with flexsearch
- Service worker enabled for offline caching
- Comments disabled
- Git info enabled for "Last Modified" dates

## Working with Content

### Adding New Chapters
1. Create both `.en.md` and `.zh.md` files in the appropriate part directory
2. Use proper naming: `part-{number}-{chapter-number}-{slug}.{lang}.md`
3. Set appropriate `weight` in frontmatter for ordering
4. Include title in frontmatter

### Translation Workflow
The maintainer translates English content chapter by chapter into Traditional Chinese. When adding or editing translations:
- Maintain parallel file structure between .en.md and .zh.md
- Keep same base filename (only language suffix differs)
- Preserve markdown formatting and footnote references
- Match the weight values between language versions
