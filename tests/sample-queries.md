# Sample Test Queries

Use these to verify the skill produces the expected output structure and risk classifications.

---

## Test 1 — Permissive, Commercial Safe

**Query:** "I want to use React (MIT) and Lodash (MIT) in my commercial SaaS. Anything I need to do?"

**Expected:**
- Risk: 🟢 Low
- Obligations: Include LICENSE/copyright notices
- Recommendation: Safe to use, just include notices
- No clarifying questions needed (context is clear)

---

## Test 2 — AGPL in SaaS (High Risk)

**Query:** "Can I use an AGPL-3.0 charting library in my proprietary SaaS backend?"

**Expected:**
- Skill asks: distribution model, commercial intent
- Risk: 🔴 High
- Obligations: Must open source entire application
- Recommendation: Avoid or find MIT/Apache alternative or buy commercial license

---

## Test 3 — GPL Internal Use (Safe)

**Query:** "We use a GPL-3.0 library for internal data processing. No external users ever touch this tool."

**Expected:**
- Risk: 🟢 Low (internal use only)
- Skill explicitly notes: copyleft does NOT trigger for internal-only tools
- No open sourcing required

---

## Test 4 — LGPL Dynamic Linking

**Query:** "We're bundling ffmpeg (LGPL-2.1) in our commercial desktop app as a separate binary."

**Expected:**
- Risk: 🟡 Medium
- Obligations: Include LGPL notice, allow binary replacement, credit ffmpeg
- Does NOT require open sourcing the app
- Recommendation: Safe with precautions — don't statically link, don't modify ffmpeg source

---

## Test 5 — No License File

**Query:** "I found a useful utility on GitHub but there's no LICENSE file. Can I use it?"

**Expected:**
- Clear statement: no license = all rights reserved = NOT open source
- Do not use without explicit permission from the author
- Recommendation: Contact the author or find an alternative

---

## Test 6 — Dual License

**Query:** "This library is dual licensed MIT / GPL-3.0. Which should I use?"

**Expected:**
- Explanation of both options
- MIT: permissive, no copyleft, just include notice
- GPL-3.0: if you want to contribute back / open source your use
- Recommendation for commercial proprietary use: choose MIT

---

## Test 7 — GPL-2.0 + Apache-2.0 Compatibility

**Query:** "Is GPL-2.0 compatible with Apache-2.0? I want to combine both in one project."

**Expected:**
- Compatibility Matrix showing ❌ Incompatible
- Explanation: Apache-2.0 has a patent termination clause that GPL-2.0 considers an "additional restriction" — the two licenses conflict
- Note: GPL-3.0 + Apache-2.0 IS compatible (GPL-3.0 explicitly allows this)

---

## Test 8 — CC License on Code

**Query:** "A dataset library I want to use is licensed CC-BY-4.0. Is this fine for my commercial product?"

**Expected:**
- Risk: 🟢 Low for the dataset/content itself
- Important caveat: CC licenses are designed for content/data, not software code
- If it's a software library using CC: flag that CC is inappropriate for code, check with the author
- If it's data: CC-BY-4.0 requires attribution, which is a manageable obligation
