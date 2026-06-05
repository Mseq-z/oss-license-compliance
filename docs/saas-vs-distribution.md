# SaaS vs Distribution — GPL vs AGPL Explained

One of the most misunderstood topics in open source licensing. This doc explains the critical distinction clearly.

---

## The Core Question

> "Does copyleft trigger if I'm building a SaaS — where users never download my software, they just use it in a browser?"

The answer depends entirely on **which license** you're using.

---

## GPL (v2 and v3) — The Distribution Trigger

GPL copyleft triggers on **distribution**. Distribution means: you send a copy of the software to someone else's machine.

| Scenario | GPL Triggered? |
|---|---|
| SaaS — users access via browser (no download) | ❌ No |
| Desktop app distributed to users | ✅ Yes |
| Mobile app in app stores | ✅ Yes |
| Docker image published publicly | ✅ Yes |
| Internal tool used only by employees | ❌ No |

**The SaaS Loophole:** If you run GPL software on your servers and users access it over a network, GPL does NOT require you to release your source code. This is why companies like Google could use GPL software internally in web services without open sourcing them.

---

## AGPL — The Network Trigger

AGPL (Affero GPL) was created specifically to close the SaaS loophole. It adds one extra trigger on top of GPL's distribution trigger:

> **"If you run a modified version of this Program on a server and let other users communicate with it there... you must provide a way for them to receive the Corresponding Source."**

| Scenario | AGPL Triggered? |
|---|---|
| SaaS — users access via browser | ✅ Yes — source must be available |
| Internal tool used only by employees | ❌ No — no "other users communicating" |
| Desktop app distributed | ✅ Yes |
| API used by external developers | ✅ Yes |

**The AGPL requires:** A prominent link (typically in the UI or API response headers) allowing any user to download the complete corresponding source code of what's running on your server.

---

## The Practical Implications

| You're building... | GPL-3.0 library | AGPL-3.0 library |
|---|---|---|
| Internal tooling (no external users) | 🟢 Safe | 🟢 Safe |
| SaaS (external users, no download) | 🟢 Safe (no distribution) | 🔴 Must open-source |
| Distributed desktop app | 🔴 Must open-source | 🔴 Must open-source |
| Open source project | 🟢 Publish under compatible license | 🟢 Publish under compatible license |

---

## Common Mistakes

**Mistake 1:** "We're SaaS, we don't distribute software, so GPL doesn't apply to us."
→ **Correct for GPL. Wrong for AGPL.**

**Mistake 2:** "We're using AGPL internally only, so it's fine."
→ **Correct if truly internal.** "Internal" means only employees/contractors of your org — not customers, external API consumers, or the general public.

**Mistake 3:** "We isolated the AGPL component behind a microservice boundary, so we're safe."
→ **Contested.** The "API boundary as a separation" argument is not universally accepted. Some lawyers think it works; others disagree. Don't rely on this without specific legal advice.

---

## What to Do If You Find AGPL in Your Stack

1. Check if the library offers a **commercial license** (many AGPL projects do — AG Grid, Grafana, etc.)
2. Find an **MIT or Apache-licensed alternative** (often exists)
3. If you must use it: publish your source code under AGPL and add a source download link to your UI
4. **Consult a lawyer** for high-value commercial situations before proceeding

---

> ⚠️ This document is informational, not legal advice.
