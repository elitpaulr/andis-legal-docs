#Readme for ANDIs legal docs
This repository supports versioned legal and policy documents for the &Improve product family.  







## 📚 Policy Versioning: Linking Old Versions — Guidance

This repository supports versioned legal and policy documents for the &Improve product family.  
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


##Slight maintenance overhead
Each time you publish a new version:

add a new vN.md file,
move the /latest/ permalink to it,
mark the previous version as archived,
update version-history.md.

This repository’s structure makes this workflow simple.

## 🧭 How Archived Versions Should Be Implemented
### 1. File structure
Each policy lives inside its own Jekyll collection:
terms/
  v1.md
  v2.md   <-- current version (owns /terms/latest/)
privacy/
  v1.md   <-- current version until v2 created
research/
  v1.md

###2. “Latest” permalink ownership
Only the current version file includes:
YAMLpermalink: /policy-name/latest/Show more lines
When publishing a new version, remove the permalink from the previous file and add it to the new one.
###3. Marking archived versions
Archived versions should include:
YAML---title: "Privacy Policy v1 (Archived)"layout: singlerobots: noindex---> ⚠️ **Archived version — not currently in effect.**  > View the latest version: /privacy/latest/Show more lines
###4. Linking from Version History
Example:
Markdown## Privacy Policy- v2 — 2026‑04: Updated minors section- v1 — 2026‑02: Initial unified Privacy Policy- **Latest:** /privacy/latest/Show more lines
Relative links work locally and on GitHub Pages due to the baseurl setup.

#📝 Summary
Linking old versions is good practice when done carefully:

✔ improves transparency
✔ supports compliance
✔ avoids user confusion with clear banners
✔ protects search results with noindex
✔ keeps a clean /latest/ endpoint for the current version

This repository is structured to make this workflow simple, safe, and auditable.