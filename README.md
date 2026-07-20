# mattsapps

Landing page for [mattsapps.xyz](https://mattsapps.xyz) — a static, dependency-free
launcher listing each app, one per subdomain.

## Why subdomains

Each app lives in its own repo and gets its own subdomain
(`app-name.mattsapps.xyz`) rather than a subpath of this site. That gives every
app its own origin, which matters once an app is wrapped as an installable
PWA or a native app (Capacitor/TWA/etc.) — separate origins mean separate
service worker scopes and separate local storage, avoiding collisions between
apps.

## Adding a new app

1. Create a new repo for the app (its own stack, its own build).
2. Give it a `CNAME` file (or `public/CNAME` if it has a build step that
   copies a `public/` dir into the build output) containing
   `app-name.mattsapps.xyz`.
3. Add a GitHub Actions workflow that builds it and deploys via
   `actions/upload-pages-artifact` + `actions/deploy-pages` — copy
   `.github/workflows/deploy.yml` from the `dinner-bell` repo (or this repo,
   for a no-build static site) as a template.
4. In the new repo's GitHub Settings → Pages: set Source to "GitHub Actions",
   then set the custom domain to `app-name.mattsapps.xyz`.
5. Add a DNS record: `app-name` → `CNAME` → `fattymatty007.github.io`.
6. Add a card to `APPS` in this repo's `index.html`, then commit and push —
   the landing page redeploys automatically.
