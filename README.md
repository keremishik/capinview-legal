# Publishing the legal pages

The two documents Play requires — a privacy policy for the listing, and both of them linked from the
purchase screen — are written and finished in this folder. What is left is hosting them, which takes
about ten minutes and needs no build step, no framework and no domain.

**The app hardcodes where they live.** `ui/subscription/LegalUrls.kt` points at:

```
https://keremishik.github.io/capinview/privacy/
https://keremishik.github.io/capinview/terms/
```

Publish to those exact URLs and nothing in the app changes. Publish somewhere else and
`LegalUrls.kt` must be edited and the app rebuilt, so it is worth matching the paths.

## What is here

```
docs/legal/
├── .nojekyll          tells GitHub Pages not to run Jekyll (which drops `_` files)
├── site.css           one stylesheet in the app's palette, light and dark
├── assets/            icon and favicon
├── index.html         landing page, links to both documents
├── privacy/index.html Privacy Policy — English and Turkish in one page
└── terms/index.html   Terms of Use — English and Turkish in one page
```

Each page carries both languages behind a toggle and opens in the reader's own language, so the Play
Console needs only one URL per document regardless of locale.

## The recipe

1. Create a **new public GitHub repository named `capinview`** on the `keremishik` account. The
   repository name is what produces the `/capinview/` path segment; a different name changes the URL.
2. Upload the contents of *this folder* — `.nojekyll`, `site.css`, `assets/`, `index.html`, `privacy/`, `terms/` — to the
   repository root, keeping the folder structure. Drag-and-drop in the GitHub web UI handles this;
   `git init && git add . && git commit && git push` does too.
3. **Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)` → Save.**
4. Wait a minute, then open all three URLs and confirm they load:
   - `https://keremishik.github.io/capinview/`
   - `https://keremishik.github.io/capinview/privacy/`
   - `https://keremishik.github.io/capinview/terms/`
5. Paste the privacy URL into **Play Console → App content → Privacy policy**, and the site root into
   the listing's Website field.

Do not upload the app's source to that repository — it is the public web root. Only these four files
belong in it.

## Before you publish, check two things

- **The contact email.** Both pages carry `kerem.ishik@gmail.com`, and this is a public web page. If
  you would rather publish a dedicated address, change it in `privacy/index.html`,
  `terms/index.html`, `index.html` and `docs/play-console-pack.md` — four files, one address.
- **The name.** Both pages name Kerem Işık as an individual developer in Türkiye. If the Play
  developer account is registered to a company instead, the documents must name the company, and
  Play checks that the name on the listing matches the one in the policy.

## Keeping them true

The privacy policy makes one strong claim — *nothing is collected, nothing leaves the device except
symbols and dates* — and it is true of v1.0.0 exactly. It stops being true the day cloud backup or
sync ships. When that happens, all three of these move together: this page, the Data safety form, and
Play's account-deletion requirement.
