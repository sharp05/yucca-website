# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static website for YuCCA Lab (Yu's Cognitive Computing and Automation Lab) at UC Merced. The site is built with vanilla HTML, CSS, and JavaScript - no build tools or frameworks required.

## Architecture

### Core Structure

The website consists of independent HTML pages with shared styling:
- `index.html` - Home page with research focus and active projects
- `publications.html` - Publications page with BibTeX parser
- `members.html` - Lab members directory
- `join.html` - Recruitment information
- `miscellaneous.html` - Lab culture and outdoor activities
- `styles.css` - Global styles with UC Merced color scheme
- `pubs.bib` - BibTeX file containing all publications

### Member Subdirectories

Individual member pages are organized in `members/<name>/`:
- `images/photo.jpg` - Profile photo
- `index.html` - Optional personal webpage
- Members can have their own CSS/JS in subdirectories

### Dynamic Features

**Header Background Rotation:**
All pages implement a rotating header background that cycles every 60 seconds. Images are loaded from `figures/images.json` which lists filenames in the `figures/` directory.

**Publications System:**
The `publications.html` page includes a custom BibTeX parser that:
- Fetches and parses `pubs.bib` at runtime
- Groups publications by year (descending order)
- Handles nested LaTeX braces in `\textbf{}` and `\textsuperscript{}`
- Converts LaTeX umlauts to Unicode characters
- Extracts conference abbreviations from venue names in parentheses
- Auto-generates colored tags based on conference/year
- Supports optional fields: `code`, `slides`, `award`

### Color Scheme

UC Merced branding colors defined in `styles.css`:
- `#002856` - Lake Yosemite Blue (primary)
- `#0091B3` - Sierra Sky Blue (links, accents)
- `#DAA900` - California Poppy Gold (borders, highlights)
- `#FFBF3C` - Golden Wheat
- `#5B5B5B` - Half Dome Slate Gray

### Member Card System

Three card types with different widths and layouts:
- **Large cards** (60% width): PI and PhD students
- **Small cards** (2-column grid): Master's and undergraduate students
- Each includes photo, name, title, education, start date, contact info

## Adding Content

### New Lab Members

Follow the template-based system described in README.md:
1. Create folder in `members/<name>/`
2. Add `images/photo.jpg` (recommended 400x400px)
3. Add entry to appropriate section in `members.html` using the role-specific template
4. If no personal webpage, remove the `<a>` tag from the name field

### Publications

Edit `pubs.bib` directly. The JavaScript parser handles:
- Standard BibTeX fields: `title`, `author`, `year`, `journal`, `booktitle`, `url`
- Custom fields: `code`, `slides`, `award`
- LaTeX formatting in any text field
- Author names in "Last, First" format (auto-converted to display format)

### Header Images

Add images to `figures/` and update `figures/images.json` with the filename (without `figures/` prefix).

## Development Workflow

This is a static site - no build process required:
1. Edit HTML/CSS directly
2. Test by opening HTML files in a browser
3. Commit and push changes
4. The PI deploys to the server manually

## Important Notes

- All HTML pages share the same header rotation JavaScript - keep it consistent when adding new pages
- Member card templates must maintain the exact CSS class structure for proper layout
- BibTeX parser uses regex for nested braces - test complex LaTeX formatting
- Avoid very large files in member subdirectories
- Profile photos should be professional headshots with reasonable dimensions
- The PI (GitHub: Orienfish) must review all pull requests before deployment

## Testing Considerations

When making changes:
- Test all pages in multiple browsers (Chrome, Safari, Firefox)
- Verify header image rotation works (check browser console for errors)
- For publication changes, validate BibTeX syntax and test LaTeX conversion
- Check responsive layout on mobile viewports (media query breakpoint: 768px)
- Ensure link colors maintain sufficient contrast for accessibility
