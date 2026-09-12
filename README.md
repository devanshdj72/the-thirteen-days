# The Thirteen Days — reader site

A self-contained, installable web app (PWA) for reading *The Thirteen Days*,
with a page-flip animation, an app cover, and offline support.

## What's in here

```
index.html   → the whole reader (styles, book text, and flip logic)
manifest.json → makes it installable ("Add to Home Screen" / desktop install)
sw.js        → service worker, caches the app so it opens offline after first visit
icons/       → app icons generated from the cover art
```

## Publish it with GitHub Pages (no build step needed)

1. Create a new GitHub repository (public repos get free Pages hosting).
   You can name it anything, e.g. `thirteen-days`.

2. Put every file in this folder into the root of that repository —
   `index.html`, `manifest.json`, `sw.js`, and the `icons/` folder,
   keeping that exact folder structure.

3. Commit and push:
   ```
   git init
   git add .
   git commit -m "The Thirteen Days — reader site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```

4. On GitHub, go to your repo's **Settings → Pages**.
   - Under "Build and deployment", set **Source** to `Deploy from a branch`.
   - Set **Branch** to `main` and folder to `/ (root)`.
   - Save.

5. GitHub will give you a live URL, usually:
   ```
   https://<your-username>.github.io/<repo-name>/
   ```
   It can take a minute or two to go live the first time.

6. Open that URL on your phone and you'll get the option to
   "Add to Home Screen" — it'll install like a real app, with the
   cover art as its icon, and will keep working even with no signal
   once it's been opened once.

## Updating the book later

If you edit the text and want to redeploy, just replace `index.html`
(the whole book is embedded inside it) and push again — no other files
need to change unless you swap the cover art, in which case regenerate
the icons too.

One thing to know: the service worker caches `index.html` aggressively
so the app works offline. If you push an update and it doesn't show up
right away for returning visitors, bump the cache name in `sw.js`
(change `thirteen-days-v1` to `thirteen-days-v2`, etc.) — that forces
everyone's browser to fetch the new version instead of serving the old
cached one.
