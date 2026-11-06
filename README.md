# noproctor

Public repository for **noproctor** - the invisible desktop answer overlay.

This repo has two jobs:

1. **Marketing site** at [noproctor.com](https://noproctor.com), served by GitHub Pages from the repo root (`main` branch).
2. **Release feed** for the desktop app. The app's auto-updater (electron-updater) reads GitHub Releases on this repo, so the app source itself (which is private) can publish signed builds here without shipping a token.

## Layout

```
index.html          landing page + Stripe checkout (product "desk")
activate/           post-checkout + magic-link activation (hands the token to the app)
privacy/  terms/    legal pages
assets/             shared stylesheet, logo, favicon
CNAME               noproctor.com
```

## Deploy

The site is static. Push to `main` and GitHub Pages publishes it. There is no build step.

## Releases

Desktop builds are published here as GitHub Releases tagged `desk-v<version>`:

- **macOS**: built, signed and notarized locally, uploaded to the matching release.
- **Windows**: built and signed in CI in the private app repo, published here automatically.

The app updates itself from the latest release on this repo.

## Backend

The site talks to one backend (the shared canvasquiz billing Function URL) for `/checkout` and `/claim`. The desktop app's `$24.99/mo` (or `$79.99/4-month`) subscription is a separate product from the browser extension; the extension subscription does not unlock it.
