# Coinrise – installable web app

This folder is the whole app. Upload the folder (not the zip itself) to any web host that serves HTTPS, and people can install it on their phone's home screen. It opens full-screen with its own icon and keeps working offline after the first visit.

## What's in here

| File | What it does |
|---|---|
| `index.html` | The app itself (three steps: See it grow, Plan it, Make it last) |
| `manifest.webmanifest` | Name, colours and icons the phone uses when it installs the app |
| `sw.js` | Service worker: saves the app so it works offline |
| `icons/` | App icons (192px, 512px, a "maskable" version for Android, and an Apple touch icon) |

## Put it online (easiest option)

1. Go to **Netlify Drop** (app.netlify.com/drop) and sign up for a free account.
2. Drag this whole folder onto the page.
3. Netlify gives you a web address straight away. You can connect your own domain later in Netlify's settings.

Other free hosts that work the same way: **GitHub Pages** and **Cloudflare Pages**. Any host is fine as long as it uses **HTTPS**; the offline feature and "install" prompt don't work over plain HTTP.

## Install it on a phone

- **iPhone (Safari):** open the web address, tap **Share**, then **Add to Home Screen**.
- **Android (Chrome):** open the web address, then tap **Install app** (or menu ⋮ → **Add to Home screen**).

## Updating the app later

1. Replace `index.html` with the new version.
2. Open `sw.js` and change `VERSION = "coinrise-v2"` to a new value, for example `"coinrise-v3"`.
3. Upload the folder again.

Step 2 matters: it tells installed copies to fetch the new version.

## Deep links

Each step has its own link, handy for marketing posts:

- `…/#money` – See it grow (coins explainer, the start)
- `…/#goal` – Plan it
- `…/#last` – Make it last

## Before you launch publicly

- The State Pension amount (£241.30 a week), income tax bands (2026/27), the £268,275 lump sum allowance, the £20,000 ISA allowance and PLSA figures are written into `index.html`. Check them each April, as they change.
- The app is educational, not financial advice. Have the wording reviewed by a compliance professional before promoting it, especially if you add links to financial products.
