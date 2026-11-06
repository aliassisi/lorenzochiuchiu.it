# Lorenzo Chiuchiù website

A static site: one page, `index.html`, with its PDFs and images in `documenti/`.
It is served from an FTP folder. PR previews use GitHub Pages (`gh-pages` branch). There is no backend and no build step.

## Layout
- `index.html`: the whole page. CSS and JS are inline. Fonts come from Google Fonts.
- `documenti/`: PDFs and scans linked from the page.
- `.github/scripts/check_links.py`: finds links to files that do not exist.

## How changes ship
1. Branch, edit, open a PR.
2. The PR gets a preview. The link is posted on the PR.
3. Merge to `main`. The "Deploy production" workflow uploads the site to the FTP folder over FTPS. It needs the secrets `FTP_SERVER`, `FTP_USERNAME`, `FTP_PASSWORD` and an optional variable `FTP_DIR`.
`.claude/`, `.github/`, `.nojekyll` and `CLAUDE.md` are not published.

## How to edit
`index.html` is the source. It is large (over 1 MB), so search for the part you need
and edit that. Do not read or rewrite the whole file.
Links to files use relative paths (`documenti/x.pdf`). Keep them relative, so the
PR preview works under a sub-path.

## Check your work
- `python3 -I .github/scripts/check_links.py .` finds missing link targets.
  Known misses go in `.github/scripts/known_broken.txt`. A hook runs it after edits.
- Run the site and look at it: use the `run-site` skill. Do not call a change done
  until you have looked at the page.

## Writing
Short, plain sentences in commits and PR text. Say what is not checked.
