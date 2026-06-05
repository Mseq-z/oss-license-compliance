# Example: Using an AGPL-3.0 Library in a SaaS Product

This example shows how the skill handles one of the most dangerous and misunderstood license scenarios — an AGPL-licensed dependency in a SaaS backend.

---

## The Query

> "We're building a SaaS analytics platform (proprietary, closed source). We want to use a data visualisation library that's licensed under AGPL-3.0. Is this okay?"

---

## Clarifying Questions Asked

1. How will you use the library? → Importing it, possibly modifying some components
2. Distribution model? → SaaS — users access via browser, no binary download
3. Commercial? → Yes, commercial SaaS startup
4. Tech stack? → Node.js backend + React frontend

---

## Compliance Report

### 🏷️ License Identity

| Field | Detail |
|---|---|
| License Name | GNU Affero General Public License v3.0 |
| SPDX ID | `AGPL-3.0-only` |
| Category | **Network Copyleft** |
| OSI Approved? | Yes |
| FSF Free? | Yes |

**Network Copyleft** means: even if you never distribute a binary, the act of *users accessing your software over a network* counts as "distribution" and triggers the copyleft obligation.

---

### 📋 Obligations

If you proceed with AGPL:

- [ ] Your **entire application's source code** must be made publicly available under AGPL-3.0
- [ ] Users must be able to download the source via a prominent link in the UI
- [ ] You must include the AGPL license text in your repository and application
- [ ] Any modifications to the AGPL library itself must be clearly documented and released

---

### 🚫 Prohibitions

- You **cannot** keep your backend proprietary while using AGPL
- You **cannot** add contractual restrictions preventing users from redistributing your source
- You **cannot** sublicense the AGPL components under different terms

---

### ⚠️ Risk Classification

**🔴 High**

This is a direct conflict with your commercial, closed-source model. AGPL-3.0 was specifically designed to close the "SaaS loophole" in GPL — the fact that you're not distributing binaries provides no protection here.

Using AGPL in a proprietary SaaS = you must open source your entire platform. For most commercial SaaS businesses, this is not viable.

---

### ✅ Recommended Action

**Avoid or replace.**

Three options:
1. **Find an MIT/Apache alternative** — most popular charting/visualisation libraries have permissive-licensed alternatives (e.g. Chart.js MIT, Recharts MIT, Apache ECharts Apache-2.0)
2. **Purchase a commercial license** — some AGPL libraries (e.g. AG Grid, QuestDB) offer a paid commercial license that removes the copyleft obligation
3. **Isolate behind an API boundary** — some legal opinions hold that AGPL doesn't propagate across a network API boundary (microservice pattern), but this is contested and you should get actual legal advice before relying on it

---

### 💡 Practical Tips

- **Audit your npm/pip tree** — AGPL dependencies sometimes appear as transitive deps you didn't intentionally add. Run `npm ls` or `pip-licenses` to surface them.
- **Add an AGPL block to your dependency policy** — tell your team and your package manager to warn or error on AGPL packages.
- When evaluating JS charting libraries, always check the license tab on npmjs.com before adding — AGPL is common in visualisation and DB tooling.

---

> ⚠️ This is informational guidance, not legal advice. For a commercial SaaS product, consult an IP lawyer before proceeding.
