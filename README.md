# colorful-github

A Chrome extension that adds a ✨ to GitHub's UI.

![screenshot](screenshot.png)

## Install

1. Clone this repo
2. Go to `chrome://extensions`
3. Enable **Developer mode** (top right toggle)
4. Click **Load unpacked** and select this folder
5. Visit any GitHub page while logged in

To pick up CSS changes, click the reload icon on the extension card in `chrome://extensions`.

## How it works

`content.css` is injected into every `https://github.com/*` page and targets specific elements with a gradient animation and custom primary button colors.

## GitHub's partial migration

GitHub is mid-migration from old server-rendered [Primer CSS](https://primer.style/css) to new [Primer React](https://primer.style/components) components. Some pages use old classes, some use new — so `content.css` targets both.

Key patterns:

- **New React components** use stable `data-*` attributes (e.g. `[data-variant="primary"]`) and semantic class names like `GlobalNav`
- **Old server-rendered pages** still use Primer CSS classes like `.Box-header`, `.btn-primary`
- **CSS module classes** (e.g. `LatestCommit-module__Box__HASH`) have unstable hashes — use `[class*="LatestCommit-module__Box"]` partial matches instead
- `!important` is required — GitHub's styles are specific enough to win otherwise
