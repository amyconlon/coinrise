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
2. Open `sw.js` and change `VERSION = "coinrise-v8"` to a new value, for example `"coinrise-v9"`.
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

## Adviser Quick Check (business demo)

`quick-check.html` is a short, branded version for advisers: four questions, one answer and a booking button. It's set up for an invented demo firm.

To make a version for a real firm, open `quick-check.html` and edit the **BRAND SETTINGS** block near the bottom: firm name, initials, colours, booking link, phone number, regulatory statement and growth assumptions. Set `demo: false` to remove the Demo badge.

To put it on the firm's website, see **Embedding a tool on a client's website** below.

## Instant Quote Estimator (trades demo)

`quote-estimator.html` is a demo for an invented decorating business. Customers add rooms, tick the work needed and see a live price range, then book a free survey.

To set it up for a real business, edit the **BRAND & PRICE SETTINGS** block near the bottom: business name, colours, booking link, phone, VAT wording, and every price (per square metre for walls and ceilings, skirting per metre, doors, wallpaper removal, condition and furniture adjustments, minimum job and the price range). Set `demo: false` to remove the Demo badge.

The prices in the demo are placeholders, not market rates.

## More demo tools and the showcase page

`tools.html` is a showcase listing every demo tool. Send its link to prospects. The demo tools are:

| File | Tool |
|---|---|
| `treatment-finder.html` | Beauty Treatment Finder quiz |
| `dog-grooming.html` | Dog grooming price checker |
| `cleaning-quote.html` | Cleaning quote (regular, deep, end of tenancy, after builders) |
| `removals-calculator.html` | Moving cost and van size calculator |
| `driving-lessons.html` | Driving lesson planner |
| `boiler-finder.html` | Boiler finder and price guide |

Each has a settings block near the bottom of the file for the business name, colours, booking link and prices. In `tools.html`, set `CONTACT.url` to your email or contact page to show the "Get in touch" button.

## Embedding a tool on a client's website

Host the tool yourself (for example on GitHub Pages), then use one of these on the client's site.

**Option 1: a button or link (works everywhere).** Link to the tool's address, e.g. `https://amyconlon.github.io/coinrise/quote-estimator.html`.

**Option 2: embed with auto-height (best).** Paste this into a Custom HTML / code block. Change the `src` address, and give each tool its own `id` if a page has more than one. The frame grows and shrinks to fit the tool, so there's no scrolling box.

```html
<iframe id="tool-quote" src="https://amyconlon.github.io/coinrise/quote-estimator.html" title="Instant quote" loading="lazy" style="width:100%;max-width:680px;height:1600px;border:0;display:block;margin:0 auto"></iframe>
<script>
window.addEventListener("message", function (e) {
  var f = document.getElementById("tool-quote");
  if (!f || e.source !== f.contentWindow || e.origin !== "https://amyconlon.github.io") return;
  if (e.data && e.data.type === "tool-height") f.style.height = e.data.height + "px";
});
</script>
```

**Option 3: embed without the script.** Some builders (for example Wix's "Embed a site" element, or WordPress.com on lower plans) don't allow scripts. Use just the `<iframe>` line with a fixed height that fits the tool on a phone (about 1600px for the estimator, 1450px for the Quick Check).

When a tool is embedded, the estimator's pinned price bar hides itself automatically, because it would sit at the bottom of the frame rather than the screen.
