# Strip — PWA (iPhone) build

A phone-friendly version of Strip: continuous-scroll CBZ reading, smooth
autoscroll, tap-to-cycle zoom (fit width / fit height / fit page), and an
on-device library with cover thumbnails and reading-progress memory.

## What's different from the desktop app

- **No text-to-speech / OCR** (as requested).
- **No `.cbr` support.** RAR extraction on desktop uses a native Node
  package; there's no equivalent that runs safely in a browser/PWA context
  without a much bigger dependency, so this build only reads `.cbz`/`.zip`.
- **No PDF support** in this build (kept out of scope to keep this a focused,
  well-tested first version).
- **Library works differently.** The desktop app watches a folder on your
  computer. iOS doesn't allow apps to do that, so this version works by
  *importing* files instead — pick one or more `.cbz` files (from the Files
  app, iCloud Drive, AirDrop, etc.) and they're copied into the app's private
  on-device storage (IndexedDB) so they're there every time you open it, no
  internet required after that.
- Ctrl+scroll zoom (desktop) is replaced by the same tap-to-cycle zoom button,
  plus your phone's native pinch-to-zoom still works everywhere.

## Hosting it (needed once, so Safari has a URL to install from)

iOS can only "Add to Home Screen" a page loaded over `https://`, not a raw
HTML file. GitHub Pages is a free, easy way to get one — same process as
before:

1. Unzip this, `cd` into the folder.
2. `git init && git add -A && git commit -m "Strip PWA"`
3. Create an empty repo on GitHub, then:
   `git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git`
   `git branch -M main && git push -u origin main`
4. On GitHub: **Settings → Pages → Deploy from a branch → main / (root)**
5. Wait ~60 seconds, then visit `https://YOUR-USERNAME.github.io/YOUR-REPO/`

## Installing on your iPhone

1. Open that URL in **Safari** (must be Safari, not Chrome — only Safari
   can install PWAs on iOS).
2. Tap the **Share** button → **Add to Home Screen** → **Add**.
3. Open it from the home screen icon like any other app. It'll launch
   full-screen, no browser bar, and works offline from then on.

## A few honest caveats

- iOS can, in rare low-storage situations, clear a web app's on-device
  storage. It's not common, but unlike a native app it's not guaranteed
  never to happen — don't rely on this as your only copy of anything
  irreplaceable.
- This was built and tested in a Chromium-based environment (no Mac/iPhone
  available on my end). The core logic — import, zip parsing, IndexedDB
  library, zoom, autoscroll, progress save/restore — was verified working
  end-to-end. iOS Safari-specific quirks (exact install prompt behavior,
  any WebKit rendering differences) haven't been tested on a real device.
  If something looks off specifically on your phone, tell me what you're
  seeing and I'll fix it.
