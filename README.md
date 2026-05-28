# I Said No — marketing & legal site

Static site hosted on GitHub Pages. Serves the support, privacy, and terms
pages that App Store Connect requires for submission (`isaidno.app` domain
not yet registered — temporary canonical home).

Live URLs once Pages is enabled:
- `https://quirag.github.io/isaidno/`              ← marketing landing
- `https://quirag.github.io/isaidno/support.html`  ← support contact + FAQ
- `https://quirag.github.io/isaidno/privacy.html`  ← Privacy Policy
- `https://quirag.github.io/isaidno/terms.html`    ← Terms of Service

## First-time setup (one-time, ~3 minutes)

1. Create a public GitHub repository called `isaidno` under your account
   (or org). The repo name MUST be `isaidno` so the project-page URL
   matches `quirag.github.io/isaidno/`.
2. From this directory:
   ```sh
   git init
   git add .
   git commit -m "Initial static site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/isaidno.git
   git push -u origin main
   ```
3. On GitHub: Repo → Settings → Pages → Build and deployment →
   Source: "Deploy from a branch" → Branch: `main` / folder: `/ (root)`.
   First deploy takes ~60 seconds.

## Updating

Edit any `.html` file, regenerate `privacy.html` / `terms.html` from the
source `.md` files via:

```sh
python3 <<'PY'
import markdown, pathlib
SITE = pathlib.Path("/Users/noxra/Desktop/App/ISaidNo/website")
LEGAL = pathlib.Path("/Users/noxra/Desktop/App/ISaidNo/code/ISaidNo/Resources/legal")
# … same template as the original convert script in commit history …
PY
```

Then `git commit && git push` — Pages auto-redeploys.

## Custom domain (later)

When the real `isaidno.app` is registered:

1. Add a `CNAME` file at the repo root with content `isaidno.app`
2. At the registrar: point `isaidno.app` A records to GitHub's IPs
   (185.199.108.153, .109.153, .110.153, .111.153) and add a `www`
   CNAME → `<username>.github.io`.
3. Update `AppURLs` in `../code/ISaidNo/ISaidNoApp.swift` and
   `AppStoreMetadata.supportURL` / `marketingURL` to drop the github.io
   prefix.

Source-of-truth for legal copy: the markdown files under
`../code/ISaidNo/Resources/legal/`. The site is a rendered mirror.
