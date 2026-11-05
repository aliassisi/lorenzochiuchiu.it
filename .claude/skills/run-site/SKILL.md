---
name: run-site
description: Serve the static site locally, screenshot it in headless Chrome, check console errors and links, and find the PR preview. Use to see a change working.
---

# Run and check the site

The repo root is the site. There is no build step.

## Serve
Start the server in the background. Use port 8801. The other site uses 8800, so both can run together.

    python3 -m http.server 8801 --bind 127.0.0.1

Check it: `curl -s -o /dev/null -w '%{http_code}' http://127.0.0.1:8801/` should print 200.
Stop it: `pkill -f "http.server 8801"`.

## Look at a page
Screenshot, with console messages:

    "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new \
      --disable-gpu --hide-scrollbars --window-size=1280,2400 --virtual-time-budget=8000 \
      --enable-logging=stderr --v=0 --screenshot=SCRATCHPAD/page.png http://127.0.0.1:8801/

Use the scratchpad folder for the PNG. Read it to see the page. Console lines contain `CONSOLE`.
Use `--window-size=420,2400` to see the mobile layout.
The page also has a dark theme. Check both.

## Check links
    python3 -I .github/scripts/check_links.py .

It exits 1 on any missing target that is not in `.github/scripts/known_broken.txt`.
The hook runs it after each HTML or CSS edit.

## Compare with the PR preview
`gh pr checks N` shows the preview run. The link is posted on the PR.
