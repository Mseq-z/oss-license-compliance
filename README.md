# 🔏 OSS License Compliance — Claude Skill

> A Claude AI skill that acts as an expert open source software license compliance advisor — helping developers and product builders understand their obligations, risks, and options when using OSS libraries.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Claude Skill](https://img.shields.io/badge/Claude-Skill-blueviolet)](https://claude.ai)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

---

## 📖 What Is This?

This is a **Claude skill** — a structured prompt + workflow definition that turns Claude into a focused, reliable OSS licensing expert.

When loaded into Claude, it enables:

- ✅ Instant license categorisation (Permissive / Weak Copyleft / Strong Copyleft / Network Copyleft)
- ✅ Obligation checklists tailored to *your specific use case*
- ✅ Risk classification (Low / Medium / High) with plain-English reasoning
- ✅ Multi-library compatibility matrices
- ✅ SaaS vs distribution vs internal-use distinctions
- ✅ Concrete "do this / avoid that" recommendations — not vague hedging

It covers 20+ common licenses including MIT, Apache-2.0, GPL-2.0/3.0, AGPL-3.0, LGPL, MPL-2.0, EUPL, CC licenses, and more.

---

## 🚀 Quickstart

### Option 1 — Use directly with Claude (claude.ai)

1. Open [claude.ai](https://claude.ai)
2. Paste the contents of [`SKILL.md`](SKILL.md) into a Project's **System Prompt** (or at the start of a conversation)
3. Ask your licensing question

### Option 2 — Use via the Anthropic API

```python
import anthropic

with open("SKILL.md") as f:
    skill_prompt = f.read()

client = anthropic.Anthropic()

response = client.messages.create(
    model="claude-sonnet-4-20250514",
    max_tokens=2048,
    system=skill_prompt,
    messages=[
        {
            "role": "user",
            "content": "I want to use ffmpeg (LGPL-2.1) in my commercial SaaS product. What are my obligations?"
        }
    ]
)

print(response.content[0].text)
```

### Option 3 — Claude Projects (Recommended for teams)

1. Create a new **Project** in Claude
2. Add `SKILL.md` as a project instruction
3. All conversations in that project will have the skill active
4. Share the project with your team

---

## 💬 Example Queries

The skill is triggered by questions like:

| Query | What you get |
|---|---|
| `"Can I use React (MIT) in my commercial app?"` | Full compliance report + action checklist |
| `"What does AGPL-3.0 mean for my SaaS backend?"` | Network copyleft explained, risk = 🔴 High |
| `"Is GPL-2.0 compatible with Apache-2.0?"` | Compatibility matrix with explanation |
| `"I'm bundling OpenSSL. What do I need to include?"` | Attribution & notice obligations |
| `"A library has no LICENSE file. Can I use it?"` | "All rights reserved" edge case handled |
| `"It's dual-licensed MIT / GPL-3.0. Which should I pick?"` | Trade-off analysis |

---

## 📋 What the Skill Does

### Workflow (inside the skill)

```
User question
     │
     ▼
Step 1 — Extract library name + license
     │
     ▼
Step 2 — Ask clarifying questions (use case, distribution model, commercial/non-commercial, tech stack)
     │
     ▼
Step 3 — Generate structured compliance report:
     │
     ├── 🏷️  License Identity (SPDX ID, category, OSI/FSF status)
     ├── 📋  Obligations checklist (contextualised to your situation)
     ├── 🚫  Prohibitions
     ├── ⚠️  Risk classification (🟢 Low / 🟡 Medium / 🔴 High)
     ├── ✅  Recommended action (plain English, direct)
     ├── 🔀  Compatibility matrix (multi-library scenarios)
     └── 💡  Practical tips
```

### Licenses Covered

| License | SPDX | Category |
|---|---|---|
| MIT | `MIT` | Permissive |
| BSD-2/3-Clause | `BSD-2-Clause` / `BSD-3-Clause` | Permissive |
| Apache-2.0 | `Apache-2.0` | Permissive (patent grant) |
| ISC | `ISC` | Permissive |
| Unlicense / WTFPL | `Unlicense` / `WTFPL` | Public Domain |
| MPL-2.0 | `MPL-2.0` | Weak Copyleft |
| LGPL-2.1 / 3.0 | `LGPL-2.1` / `LGPL-3.0` | Weak Copyleft |
| CDDL-1.0 | `CDDL-1.0` | Weak Copyleft |
| EUPL-1.2 | `EUPL-1.2` | Weak/Network Copyleft |
| GPL-2.0 / 3.0 | `GPL-2.0-only` / `GPL-3.0-only` | Strong Copyleft |
| AGPL-3.0 | `AGPL-3.0-only` | Network Copyleft |
| CC-BY-4.0 / CC-BY-SA-4.0 / CC0 | Various | Content licenses |

---

## 📁 Repository Structure

```
oss-license-compliance/
│
├── SKILL.md                        # ← The skill prompt (load this into Claude)
├── README.md                       # This file
│
├── examples/
│   ├── saas-agpl-example.md        # AGPL in a SaaS product walkthrough
│   └── multi-library-example.md    # Compatibility matrix example
│
├── docs/
│   └── saas-vs-distribution.md     # GPL vs AGPL for SaaS explained
│
└── tests/
    └── sample-queries.md           # Test queries + expected output structure
```

## 🧩 Edge Cases Handled

The skill is specifically designed to handle tricky, commonly misunderstood scenarios:

- **Internal use only** → Copyleft does NOT trigger. Clearly explained.
- **SaaS / no binary distribution** → GPL doesn't trigger, but AGPL does. Critical distinction made explicit.
- **Dynamic vs static linking of LGPL** → Guidance on when you're safe.
- **Modified the library itself** → Copyleft now applies to those files.
- **"GPL-2.0 or later" clause** → User can comply with any version; trade-offs explained.
- **No license file** → All rights reserved. The skill flags this and advises against use.
- **Dual licensed** → Explains both options and helps user choose.
- **Transitive dependencies** → Tips on npm/pip/Maven dependency license scanning.

---

## 🔧 Customising the Skill

You can extend `SKILL.md` for your organisation's needs:

- **Add internal policies** — e.g. "our company policy prohibits any AGPL dependency"
- **Add approved/blocked license lists** — pre-approved permissive licenses, blocked copyleft ones
- **Add jurisdiction context** — EU-specific considerations, US export control notes
- **Integrate with CI** — use the API approach above in a GitHub Action to scan new PRs

---

## ⚠️ Disclaimer

This skill provides **informational guidance**, not legal advice. For high-stakes commercial deployments, complex multi-license scenarios, or any situation with significant legal or financial risk, consult a qualified IP or software licensing attorney.

---

## 📜 License

This skill definition (prompt + documentation) is released under the [MIT License](LICENSE).

It is not affiliated with or endorsed by Anthropic.
