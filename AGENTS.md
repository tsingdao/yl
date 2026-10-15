# AGENTS.md

## Project type

Static HTML/CSS course portfolio. No build tools, no package manager, no framework, no tests. Open any `.html` file directly in a browser to preview.

## Structure

- `index.html` — portfolio landing page linking to all exercises
- Numbered HTML files (`2-1.html`, `3-1.html`, …) — individual course exercises in progression order
- `img/` — images referenced by exercises via relative paths (`./img/…`)
- `css.css` — minimal shared stylesheet; only referenced by `5-1 层叠与继承.html`

## Conventions

- All content is in Chinese (student: 袁磊, course: 高级网页设计)
- Most pages use inline `<style>` blocks, not external stylesheets
- No external dependencies or CDN links — everything is self-contained
- Some filenames contain Chinese characters and spaces (e.g., `7-1 上图下文.html`); links to these in `index.html` are URL-encoded (e.g., `./7-1%20%E4%B8%8A%E5%9B%BE%E4%B8%8B%E6%96%87.html`)

## Adding a new exercise

1. Create a new `.html` file following the numbering scheme
2. Add a `<link>` entry in `index.html` inside the `<nav class="works">` section
3. URL-encode the filename in the `href` if it contains non-ASCII characters or spaces

## Prompt logging

- Before executing any task, append the user's prompt to `yuan_prompt.md` (do not overwrite existing content)
- Include the timestamp, model name, and prompt content for each entry
