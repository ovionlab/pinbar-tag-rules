# Pinbar Tag Rules

| | |
|---|---|
| **Current version** | `1.0.0` |
| **Updated** | 2026-05-30 |
| **Rules file** | [`tag-rules.json`](./tag-rules.json) |

Auto-tagging rules for [Pinbar](https://github.com/ovionlab/pinbar) — a native macOS bookmark manager.

---

## What is this?

When you save a bookmark in Pinbar, the app automatically suggests relevant tags based on the URL and page title. This repository contains the rules that drive those suggestions.

By hosting the rules separately from the app, they can be updated and improved without requiring a new app release.

---

## How it works

The rules file contains two types of rules:

**Domain rules** — matched against the website's domain:
```json
"github.com": ["github", "code"],
"youtube.com": ["video"]
```

**Keyword rules** — matched against the URL or page title:
```json
{ "keyword": "docker", "tag": "docker" },
{ "keyword": "tutorial", "tag": "tutorial" }
```

Pinbar checks for updates weekly and downloads the latest version automatically. You can also trigger a manual update from **Preferences → Tags → Check Now**.

---

## Using a custom rules file

You can host your own rules file and point Pinbar to it:

1. Copy `tag-rules.json` from this repo
2. Edit the rules to your liking
3. Host the file somewhere publicly accessible (GitHub raw, CDN, your own server)
4. In Pinbar → **Preferences → Tags → Rules URL** — paste your URL

The file must be valid JSON matching this schema:

```json
{
  "version": "1.0.0",
  "updatedAt": "YYYY-MM-DD",
  "domainRules": {
    "example.com": ["tag1", "tag2"]
  },
  "keywordRules": [
    { "keyword": "some word", "tag": "sometag" }
  ]
}
```

Pinbar uses semantic versioning to compare versions and only downloads if the remote version is newer than the cached one.

---

## Contributing

Pull requests are welcome. To add or improve rules:

1. Fork this repo
2. Edit `tag-rules.json`
3. Bump the `version` field (e.g. `1.0.0` → `1.0.1`)
4. Update the `updatedAt` date
5. Open a PR with a short description of what you added

Please keep tags **lowercase**, **short** (1–2 words), and **broadly useful** — avoid overly specific or personal tags.

---

## Changelog

### 1.0.0 — 2026-05-30
- Initial release
- 40+ domain rules: GitHub, Stack Overflow, YouTube, Reddit, Figma, npm, PyPI, cloud providers (AWS, GCP, Azure), AI tools, JS frameworks and more
- 35+ keyword rules covering common tech stacks and frameworks
