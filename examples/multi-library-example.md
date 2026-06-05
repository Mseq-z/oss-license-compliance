# Example: Multi-Library Compatibility Matrix

This example shows how the skill handles a common real-world scenario — a Node.js web app using several open source libraries with different licenses.

---

## The Query

> "I'm building a commercial Node.js web app (SaaS). Here are my main dependencies: Express (MIT), Lodash (MIT), Mongoose (MIT), Moment.js (MIT), and I want to add a PDF generation library — pdfkit (MIT) and also wkhtmltopdf which wraps a LGPL binary. What are my obligations? Are all these compatible?"

---

## Compatibility Matrix

| Library | License | Your App (Proprietary) | Notes |
|---|---|---|---|
| Express | MIT | ✅ Compatible | Include LICENSE file |
| Lodash | MIT | ✅ Compatible | Include LICENSE file |
| Mongoose | MIT | ✅ Compatible | Include LICENSE file |
| Moment.js | MIT | ✅ Compatible | Include LICENSE file |
| pdfkit | MIT | ✅ Compatible | Include LICENSE file |
| wkhtmltopdf (binary) | LGPL-3.0 | ⚠️ Conditional | See notes below |

---

## The LGPL Binary — What You Need to Know

wkhtmltopdf is a standalone binary wrapped by your Node.js code via a child process. This is **dynamic linking** (or more accurately, process-level invocation), which is generally the safest way to use LGPL software.

### ⚠️ Risk: 🟡 Medium

**Obligations for the LGPL binary:**
- [ ] Include the LGPL-3.0 license text in your distribution / documentation
- [ ] Credit wkhtmltopdf in your app's acknowledgements or legal notices page
- [ ] If you distribute the binary bundled with your app (e.g. packaged Electron app, Docker image), ensure users can replace the wkhtmltopdf binary with their own version
- [ ] Do NOT modify the wkhtmltopdf source code — if you do, you must release those modifications

**You do NOT need to:**
- Open source your Node.js application
- Release your application code
- Change your proprietary license

---

## Overall Obligation Checklist

For a SaaS Node.js app using all the above:

- [ ] Include a `LICENSES` or `NOTICE` file listing all dependencies and their licenses
- [ ] For MIT packages: include each package's copyright line and license text (most teams use `license-checker` or `legally` to auto-generate this)
- [ ] For wkhtmltopdf: include LGPL-3.0 license text and attribution
- [ ] Surface acknowledgements in your app (e.g. `/legal` page or "About" section)

---

## 💡 Practical Tips

1. **Automate license checks in CI** — use `license-checker` (npm) to scan your dependency tree and fail the build if a new GPL/AGPL package appears:
   ```bash
   npx license-checker --onlyAllow 'MIT;Apache-2.0;BSD-2-Clause;BSD-3-Clause;ISC;LGPL-3.0'
   ```

2. **Generate a NOTICES file automatically:**
   ```bash
   npx license-checker --csv --out NOTICES.csv
   ```

3. **Watch for transitive deps** — your direct dependencies might pull in something with a different license. Always run the full tree scan, not just top-level.

---

> ⚠️ This is informational guidance, not legal advice.
