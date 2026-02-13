#Readme for ANDIs legal docs

## 🚀 Publish Workflow (Policies & Versioning)

This repo hosts the versioned legal documentation for the &Improve product family using Jekyll (Minimal Mistakes) + GitHub Pages.  
Follow this workflow to publish new versions safely, keep `/latest/` stable, and archive older versions correctly.

---

### 0) Prerequisites (local dev)

```
bash
# One-time setup (macOS)
brew install ruby
gem install bundler

# Install dependencies in the repo
bundle install

# Run local server (dev mode: no baseurl)
bundle exec jekyll serve --config _config.yml,_config_local.yml
# Open http://127.0.0.1:4000/
```

Tip: Use the alias jdev if you’ve added it to ~/.zshrc:

```
alias jdev="bundle exec jekyll serve --config _config.yml,_config_local.yml"
jdev
```

### 1) Structure recap

#### Collections:

terms/ — Terms of Use & Conditions (versioned: v1.md, v2.md, …)  
privacy/ — Privacy Policy (versioned)  
research/ — Research & Corpus Data Use Statement (versioned)  


“Current” version owns the /…/latest/ permalink.
Older versions stay addressable at their versioned paths and are visibly archived.

Example:
```
terms/
  v1.md
  v2.md   # <- has: permalink: /terms/latest/
privacy/
  v1.md   # <- has: permalink: /privacy/latest/ (until v2 exists)
research/
  v1.md   # <- has: permalink: /research/latest/
```

### 2) Creating a new version

1. Duplicate the previous version file and rename it, e.g. privacy/v2.md.
2. Move /latest/:
- Remove permalink: /privacy/latest/ from the old file.
- Add permalink: /privacy/latest/ to the new file.
3. Update front matter:

```
---
title: "Privacy Policy v2"
permalink: /privacy/latest/
layout: single
---
```

### 4. Edit the content as required (date, sections, links, minors’ safeguards, etc.).

### 5.) Mark the previous version as archived:

- Optional title tweak: "Privacy Policy v1 (Archived)"
- Add robots: noindex in front matter
- Add an archive notice at the top:

```
> ⚠️ **Archived version — not currently in effect.**
> View the latest: [/privacy/latest/](/privacy

```

### 3) Update the Version History page
Open version-history.md and add entries with links:


> ## Privacy Policy
> - v2 — 2026‑04: Updated minors section and public datasets note.
> - v1 — 2026‑02: Initial unified Privacy Policy.
> - **Latest:** /privacy/latest/

Reminder: The Version History page must have a directory permalink to avoid 404:

```
---
layout: single
title: "Version History"
permalink: /version-history/
---
```

### 4) Local QA checklist

- Routes resolve:
    - /terms/latest/, /privacy/latest/, /research/latest/
    - Archived routes, e.g. /privacy/v1/
- Version History links work and point to the intended versions.
- Archived pages:
  - Show the warning banner
  - Include robots: noindex in front matter
- Content regressions:
  - Minors’ protections reflect current policy (e.g., no public release of minors’ content)
  - Research statement matches current dataset publication/licence practice
- Build cleanly:

```
bundle exec jekyll clean
jdev
```

### 5) Commit, PR, and merge

```
git checkout -b release/privacy-v2
git add .
git commit -m "Privacy Policy v2: minors/public datasets update; archive v1; update version history"
git push -u origin release/privacy-v2
```

Open a PR:

- Title clearly states which policy and version.
- PR description includes a brief change summary and links to relevant Jira/Ticket (if any).
- Request review from Legal/Governance.

After approval, merge to main.

### 6) Publish on GitHub Pages (production)

GitHub Pages auto-builds from main.

- Watch Actions → pages-build-deployment for a green check.
- Visit the production URLs (with cache-buster if needed):

```
https://<username>.github.io/<repo>/privacy/latest/?v=1
https://<username>.github.io/<repo>/version-history/?v=1
```
If you see a 404 on Version History:

- Ensure the trailing‑slash permalink is present (see step 3).


### 7) Rollback (if needed)

If a new version must be reverted:

- Re-open the previous version file (e.g., privacy/v1.md) and restore:
```
permalink: /privacy/latest/
```

- Mark the problematic version as archived (and remove its permalink).
- Update version-history.md with a rollback note.
- Commit/push and confirm production rebuild.


### 8) SEO and discoverability

All archived versions must include:

```
robots: noindex
```

- Latest versions should remain indexable (default).
- Version History page is indexable, but it only links to noindex archives and to /latest/.


### 9) Accessibility & clarity

- Use clear headings and summaries.
- Keep parent/guardian language visible where relevant (e.g., minors exclusions from public datasets).
- Prefer British English and consistent legal labels (“Terms of Use & Conditions”).


### 10) Source of truth for “current” versions

- The only canonical location for the current policy is:
    - /terms/latest/
    - /privacy/latest/
    - /research/latest/


Any in‑product links (onboarding, settings, footer) must point to these stable endpoints.


### 11) Common pitfalls & fixes

- 404 at /version-history/ → Add permalink: /version-history/ to front matter.
- Two files claim /latest/ → Remove the permalink from the older file.
- Links resolve to the site root → Ensure baseurl is set in _config.yml and "" in _config_local.yml.
- Local/production mismatch → Always test with cache‑buster (?v=123) and check GitHub Pages build logs.


### 12) Quick publish checklist (copy/paste)
  1. New version file created (vN.md)
  2. permalink: /…/latest/ moved to the new file
  3. Previous version marked archived + robots: noindex + banner
  2. version-history.md updated with links
  3. Local build clean; routes verified
  4. PR raised, reviewed, merged
  5. GitHub Pages build green
  6. In‑product links confirm /latest/ endpoints



# Next steps:

## 📚 Policy Versioning: Linking Old Versions — Guidance
 
A common question is whether **old versions** of these documents should be linked directly from the **Version History** page.

### ✅ Recommendation
**Yes** — link old versions from the Version History page, but with safeguards to avoid user confusion and search‑engine indexing of outdated content.

---

## ✔ Pros of Linking Old Versions

### Transparency and trust
Providing archived versions creates a clear, auditable history of what changed and when.  
It aligns with Cambridge’s values and with expectations of educational institutions, researchers, and regulators.

### Legal defensibility
Keeping historical versions publicly accessible helps demonstrate:
- what policies were in force at a given time,
- what users agreed to,
- how disclosures evolved.

This supports compliance with UK GDPR transparency obligations.

### Institutional and research workflows
Schools, auditors, and academic partners often need to confirm older versions of policies, especially across school years or research study periods.

---

## ❗ Cons and Mitigations

### Users might read the wrong version  
**Mitigation:** Add a clear banner to archived versions:

> ⚠️ Archived version — not currently in effect.  
> View the latest version at `/…/latest/`.

### Search engines could index outdated versions  
**Mitigation:** Add this front‑matter to archived files:yaml robots: noindex


#### Slight maintenance overhead
Each time you publish a new version:

1. add a new vN.md file,
1. move the /latest/ permalink to it,
1. mark the previous version as archived,
1. update version-history.md.

This repository’s structure makes this workflow simple.

## 🧭 How Archived Versions Should Be Implemented
### 1. File structure
Each policy lives inside its own Jekyll collection:

```
terms/
  v1.md
  v2.md   <-- current version (owns /terms/latest/)
privacy/
  v1.md   <-- current version until v2 created
research/
  v1.md
```

### 2. “Latest” permalink ownership

Only the current version file includes:
- YAMLpermalink: /policy-name/latest/Show more lines
When publishing a new version, remove the permalink from the previous file and add it to the new one.

### 3. Marking archived versions

Archived versions should include:
- YAML
```
---
title: "Privacy Policy v1 (Archived)"
layout: singlerobots: noindex
---
```

⚠️ **Archived version — not currently in effect.**  > View the latest version: /privacy/latest/Show more lines

### 4. Linking from Version History
Example:

```
## Privacy Policy- v2
> — 2026‑04: Updated minors section
> - v1 — 2026‑02: Initial unified Privacy Policy
> - **Latest:** /privacy/latest/Show more lines
```

Relative links work locally and on GitHub Pages due to the baseurl setup.

## 📝 Summary
Linking old versions is good practice when done carefully:

- ✔ improves transparency
- ✔ supports compliance
- ✔ avoids user confusion with clear banners
- ✔ protects search results with noindex
- ✔ keeps a clean /latest/ endpoint for the current version

This repository is structured to make this workflow simple, safe, and auditable.




















