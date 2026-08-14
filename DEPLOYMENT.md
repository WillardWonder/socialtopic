# Deployment Notes

## GitHub Pages

This repository is already structured for GitHub Pages.

The included workflow publishes the repository root as a static site.

### First deployment

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Set the source to **GitHub Actions**.
4. Open the **Actions** tab and confirm the `Deploy SignalScope to GitHub Pages` workflow completed successfully.

## Why this app works on Pages

SignalScope does not require a build step or application server.

`index.html` contains:

- the UI,
- styles,
- JavaScript,
- API adapters,
- interpretation logic,
- local preference memory.

All state is kept in the browser with `localStorage`.

## Production caveats

GitHub Pages is static hosting. It cannot safely hold private API keys.

If you add authenticated sources later, do not put secrets in `index.html`.

Use a serverless backend such as:

- Cloudflare Workers,
- Vercel Functions,
- Netlify Functions,
- AWS Lambda,
- or another small API gateway.

Good candidates for backend connectors include:

- Reddit OAuth,
- YouTube API,
- SEC request normalization / caching,
- higher-volume OpenFEC access,
- rate-limit caching across all sources.

## Custom domain

GitHub Pages supports custom domains from repository settings.

If you use one, GitHub can create and manage the `CNAME` file for you.
