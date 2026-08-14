# SignalScope

SignalScope is a static, browser-based OSINT exploration app derived from the topic-matching / dynamically refreshed topic-node concepts in US 2020/0265070 A1.

A user enters a topic, company, technology, or public issue. SignalScope queries public data sources, builds a live evidence map, and explains the result in plain language.

## What it does

The default interface summarizes a topic using four understandable questions:

- **Are people talking about it?**
- **Are people looking it up?**
- **Is the media covering it?**
- **Are experts or institutions acting?**

It then shows:

- a plain-English takeaway,
- cautious implications,
- actual source records behind the summary,
- recurring cross-source concepts,
- and a technical/patent explanation for advanced users.

## Live public data sources

The current static prototype can query, when available from the browser:

- Bluesky public search
- Wikipedia / Wikimedia pageviews
- GDELT news
- OpenAlex
- GitHub public repository search
- ClinicalTrials.gov
- USAspending
- OpenFEC

Some APIs impose anonymous rate limits or may temporarily reject browser requests. SignalScope reports source failures instead of fabricating results.

## Privacy / safety design

SignalScope is intentionally designed for topic- and entity-level public-data research.

It does **not**:

- build personal political dossiers,
- join named people's social activity to voter-registration records,
- infer private traits from public records,
- or use private / credentialed data sources.

## Run locally

Because this app is static, you can open `index.html` directly in a browser.

For more reliable browser API behavior, serve it over HTTP:

```bash
python3 -m http.server 8000
```

Then visit:

```text
http://localhost:8000
```

## Deploy to GitHub Pages

### Option A — GitHub Actions (included)

1. Create a new GitHub repository.
2. Upload the contents of this folder to the repository root.
3. Commit and push to the `main` branch.
4. In GitHub, open **Settings → Pages**.
5. Under **Build and deployment**, select **GitHub Actions**.
6. The included workflow will publish the site automatically.

The site will normally appear at:

```text
https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/
```

### Option B — Deploy from branch

If you prefer not to use Actions:

1. Delete `.github/workflows/deploy-pages.yml`.
2. Open **Settings → Pages**.
3. Choose **Deploy from a branch**.
4. Select `main` and `/ (root)`.
5. Save.

## Important API notes

This is a client-side research prototype. No API secrets are bundled.

For a larger public deployment, the recommended next architecture is:

- keep the GitHub Pages frontend,
- add a small serverless proxy for APIs that need keys, headers, caching, or stricter rate limits,
- store secrets only in the backend,
- add request caching,
- and log source freshness / failure state.

In particular, sources such as Reddit, YouTube, or some SEC workflows are better added through authenticated or backend connectors rather than embedding credentials in browser JavaScript.

## Files

```text
.
├── index.html
├── .nojekyll
├── README.md
├── DEPLOYMENT.md
└── .github/
    └── workflows/
        └── deploy-pages.yml
```

## Data interpretation warning

SignalScope does not treat counts from unrelated datasets as equivalent measurements.

For example:

- 30 social posts,
- 30 academic papers,
- and 30 government awards

are different kinds of observations.

The app keeps raw source metrics separate and uses only directional heuristics for its plain-language summaries.

## Patent connection

The app preserves the patent's functional pattern:

1. establish a **current focus**,
2. seek matching **topic nodes**,
3. point those nodes to relevant destinations,
4. update the living topic structure from current activity,
5. and use preferences / feedback to refine future ranking.

SignalScope translates that logic from social chat-room matching into public-data topic intelligence.
