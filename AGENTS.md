# AGENTS.md

## What this repo is

Static HTML/CSS coursework portfolio for a Chinese "高级网页设计" class (student: 赵婉彤/zwt). No build system, no package manager, no tests, no CI, no framework. Pages are opened directly in a browser. Do not add npm/build tooling unless explicitly asked.

## Layout

- `index.html` — styled hub page linking every exercise; the site entrypoint.
- `N-L.html` / `N-L名称.html` — one standalone exercise per lesson (chapter-lesson naming, e.g. `9-1transition.html`, `5-1层叠与继承.html`). Most are self-contained with inline `<style>`.
- `css.css` — tiny shared stylesheet used only by early exercises (currently just `5-1层叠与继承.html`). Do not assume new pages link it.
- `img/` — JPG assets, referenced with relative paths (`img/1.jpg` or `./img/1.jpg`).

## Conventions that are easy to break

- Every exercise page must be linked from `index.html` (the `.work` card grid, ~line 244+). Adding a page without the link makes it invisible.
- `4-1 css2.html` has a literal space in its filename; it must stay URL-encoded as `4-1%20css2.html` in links. Other filenames contain Chinese characters — link them with the exact filenames.
- Content, comments, and `lang` attributes are Chinese coursework; titles like "Document" are intentionally left as-is by the student. Do not "clean up", translate, or normalize pages unless asked.
- Each page demonstrates one specific lesson (flex, transition, animation, selectors, etc.). Treat pages as independent exercises — avoid shared refactors or cross-page CSS extraction unless asked.
- There is no verification step: review changes by opening the affected HTML file in a browser. Relative image paths break if files move out of the root.
