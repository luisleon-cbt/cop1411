# COP1411 Algorithmic Thinking: interactives

Interactive simulations for COP1411 (CBT Technology Institute, program course). Each week has self-contained HTML pages: an explorer (Interactive A) and a scored challenge (Interactive B). The Canvas pages link to them through GitHub Pages.

Live site: https://luisleon-cbt.github.io/cop1411/

## Structure

| Folder | Topic | Interactive A | Interactive B |
|---|---|---|---|
| week1 | What an algorithm is | algorithm-flow-explorer.html | order-the-steps.html |
| week2 | Decisions | decision-router.html | predict-the-path.html |
| week3 | Repetition | loop-tracer.html | trace-table-challenge.html |
| week4 | Decomposition and the final project | function-and-sort-board.html | debug-challenge.html |

## Publishing

1. Push this folder to the `main` branch of `luisleon-cbt/cop1411`.
2. In the repository, open Settings, then Pages, and set Source to "Deploy from a branch", branch `main`, folder `/ (root)`.
3. Each page is then live at `https://luisleon-cbt.github.io/cop1411/weekN/<file>.html`.

The pages load the CBT logo from `luisleon-cbt/items`, and GSAP and fonts from public CDNs. The boards are SVG drawn and animated with JavaScript; the pages need no build step.
