# Six Animals — Field Ledger

A self-contained, installable web app. No build step, no dependencies to install — just static files.

## Files
- `Six Animals.html` — the app itself
- `index.html` — a one-line redirect to `Six Animals.html`, so your GitHub Pages root URL still works (GitHub Pages only auto-serves a file literally named `index.html`)
- `manifest.json` — makes it installable (name, icon, colors)
- `sw.js` — service worker; handles offline fallback and auto-updates
- `icon-192.png`, `icon-512.png` — app icons

## 1. Put it on GitHub

1. Create a new repository on GitHub (public or private — Pages works either way on a paid plan; public repos get Pages free).
2. Upload all six files in this folder to the root of that repository (or `git push` them) — including the space in "Six Animals.html" exactly as named.

## 2. Turn on GitHub Pages

1. In the repo, go to **Settings → Pages**.
2. Under "Build and deployment", set **Source** to "Deploy from a branch".
3. Pick your default branch (usually `main`) and folder `/ (root)`, then **Save**.
4. GitHub gives you a URL like `https://yourusername.github.io/your-repo-name/` — that's your live app. Visiting it lands you on `index.html`, which immediately forwards you to `Six Animals.html`.

## 3. Install it on your PC

1. Open that URL in Chrome or Edge — **it has to be the actual `https://` GitHub Pages URL, not a file opened by double-clicking it on your computer.**
2. Click the **install icon** in the address bar (or the browser menu → "Install Six Animals" / "Apps → Install this site as an app").
3. It now opens in its own window, with its own icon, like a regular desktop app — no browser bar.

### Why the install button might not show up
The install prompt only appears when three things are true: a valid manifest, an active service worker, and the page loaded over a secure origin (`https://` or `localhost`). Opening the HTML file directly from your file system (`file://...`) fails that third condition — browsers block service workers on `file://` for security reasons — so no install icon appears no matter how correct the files are. Once it's live on the GitHub Pages URL, this resolves itself; no code change needed.

## 4. How auto-update works

The service worker (`sw.js`) always tries the network first for the app's HTML. So:

- Every time you edit a file and `git push` to the branch GitHub Pages watches, the live URL updates immediately (GitHub Pages deploys are usually live within a minute).
- The next time you open the installed app **while online**, it fetches the new version straight away and reloads once automatically.
- If you're offline, it falls back to the last version it had cached, so it still works without internet — it just won't have that day's changes until you're back online.

No manual "check for updates" step, no rebuild, no re-install — push to GitHub, reopen the app, and it's current.

## Notes

- If you rename the repo or move it into a subfolder, double check the paths in `manifest.json` (`start_url`, `scope`) and `sw.js` (`CORE_FILES`) still resolve correctly relative to where the files end up.
- The app itself has an in-app **Reset board** button on the Points panel — that's separate from updating the app; it only clears your logged rounds.

