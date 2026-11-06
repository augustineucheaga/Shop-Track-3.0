# ShopTrack

A mobile-first app for planning market and grocery trips and keeping track of what things cost. It works offline, needs no account, and installs on a phone like a normal app.

**Live app:** https://shop-track-3-0.vercel.app/

## Why I built it

Market prices keep changing, and it is hard to remember what you paid last time or whether you stayed within budget. ShopTrack keeps a list for each trip, adds up the cost as you go, and remembers the prices for next time.

## Features

- **Trips with a budget:** start a trip, set a budget and see spent versus remaining live. The progress bar turns red when you go over.
- **Fast list building:** add items with quantity, unit and price, and pick from a swipeable "frequently bought" row of your usual items.
- **Price history:** every finished trip feeds a price history with a small trend chart for each item.
- **Calendar:** schedule future trips and get a reminder notification.
- **Restock suggestions:** ideas for what to buy next, based on your past trips. A real AI service can be plugged in (see below).
- **Share a list:** send a trip to another ShopTrack user as a link.
- **Backup:** export and import all your trips as a file.
- **Settings:** light, dark or system theme, seven currencies (₦, $, £, €, GHS, KES, ZAR) and a choice of measurement units.
- **Works offline** through a service worker, and **your data stays on your device** (nothing is sent to a server).

## Tech

| Part | Used |
|---|---|
| App | HTML, CSS and vanilla JavaScript (a single `script.js` that renders each screen) |
| Storage | `localStorage` in the browser, so there is no backend and no sign-up |
| Offline and install | Service worker and web app manifest (PWA) |
| Theming | CSS custom properties, with light, dark and system modes |
| Hosting | Vercel, deployed from this repo |

## Run it locally

No build step. Serve the folder so the service worker can register (`localhost` counts as secure):

```bash
python3 -m http.server 3000
```

Then open http://localhost:3000. To install it as an app on a phone, open the live site in the browser and use **Add to Home Screen**.

## Optional: real AI suggestions

By default, suggestions come from your own history. To use an AI service, host a small endpoint and set it before `script.js` loads:

```html
<script>window.SHOPTRACK_AI_ENDPOINT = "https://your-server.example/suggest";</script>
```

ShopTrack sends `POST {"prompt": "..."}` and expects `{"suggestions": ["item", "item", ...]}` back. The key stays on your server, never in the page. If the call fails, it quietly falls back to the local suggestions.

## Known limits

- Shared lists are encoded in the link itself, so both people need to open the same hosted address.
- Because there is no backend, clearing the browser's data clears your trips. Use **Export** to keep a copy.

## Files

| File | What it does |
|---|---|
| `index.html` | App shell and early theme setup |
| `script.js` | All app logic and screens |
| `styles.css` | Styling and themes |
| `service-worker.js` | Offline caching |
| `ERROR_REPORT.md` | Notes from review rounds: what was fixed and what is still worth improving |

## Credits

Designed and built by Kidddarts (Augustine Ucheaga). Contact: augustineucheaga@gmail.com
