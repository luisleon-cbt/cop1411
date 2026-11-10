# COP1411 Algorithmic Thinking: interactives

Interactive simulations for COP1411 (CBT Technology Institute, program course). Each week has self-contained HTML pages: an explorer (Interactive A) and a scored challenge (Interactive B). The Canvas pages link to them through GitHub Pages.

Live site: https://luisleon-cbt.github.io/cop1411/

## Structure

| Folder | Topic | Interactive A | Interactive B |
|---|---|---|---|
| week1 | Algorithms and decisions | flowchart-runner.html | cover-every-branch.html |
| week2 | Loops and data structures | loop-runner.html | load-the-van.html |
| week3 | Functions and efficient algorithms | function-calls.html | count-the-steps.html |
| week4 | Recursion and the final project | recursion-runner.html | bug-hunt.html |

## Publishing

1. Push this folder to the `main` branch of `luisleon-cbt/cop1411`.
2. In the repository, open Settings, then Pages, and set Source to "Deploy from a branch", branch `main`, folder `/ (root)`.
3. Each page is then live at `https://luisleon-cbt.github.io/cop1411/weekN/<file>.html`.

The pages load the CBT logo from `luisleon-cbt/items`, and GSAP, Prism, and fonts from public CDNs, and Python itself (Pyodide, about 10 MB) the first time a Try it box is run. The flowcharts are SVG drawn and animated with JavaScript; the pages need no build step.
