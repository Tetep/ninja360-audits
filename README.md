# Ninja-360 Audits

Internal sales archive for every visibility audit Ninja-360 has produced.

**Live URL (after deploy):** https://audits.ninja360.net/
**Hosting:** Cloudflare Pages (auto-deploy on push to `main`)
**Access:** Private — `noindex,nofollow` on every page. Unguessable URLs unless you share them. Add Cloudflare Access (free, 50-user) if/when login gating becomes useful.

---

## What lives here

Every Ninja-360 visibility audit report, organized by client slug:

```
.
├── index.html              ← private landing page — list of all audits
├── README.md
├── .gitignore
└── {client-slug}/
    └── index.html          ← the audit report itself
```

URL pattern: `https://audits.ninja360.net/{client-slug}/`

---

## How to add a new audit

After running `/ninja360-visibility-analyzer` + `/ninja360-audit-report-publisher`:

1. Create a new folder: `mkdir [client-slug]`
2. Save the audit HTML as `[client-slug]/index.html`
3. Update root `index.html` — add a new card to the audits list (copy an existing row, swap fields)
4. Commit + push:
   ```bash
   git add .
   git commit -m "audit: add [client-name]"
   git push
   ```
5. Cloudflare Pages auto-deploys in ~60 seconds
6. Live at `audits.ninja360.net/[client-slug]/`

---

## Client slug rules

Same as other Ninja-360 systems:
- lowercase
- spaces → hyphens
- strip punctuation (`'`, `.`, `,`, `&`, `LLC`, `Inc`)
- drop leading "the"
- max 60 chars

Examples:
- "Free Flowin' Libations" → `free-flowin-libations`
- "Blue Sparrow Lawn & Landscape, LLC" → `blue-sparrow-lawn-landscape`
- "Dr. Smith's Family Dental" → `dr-smiths-family-dental`

---

## Deploy: Cloudflare Pages → `audits.ninja360.net`

One-time setup:

1. Cloudflare dashboard → Workers & Pages → Create application → Pages → **Connect to Git**
2. Select repo `Tetep/ninja360-audits`
3. Branch: `main`
4. Build settings:
   - **Framework preset:** None
   - **Build command:** (leave blank)
   - **Build output directory:** `/`
5. Save and Deploy → CF assigns a `*.pages.dev` URL
6. Project → Custom domains → Add `audits.ninja360.net` → CF auto-creates the CNAME on the `ninja360.net` zone

After that, every `git push` to `main` auto-deploys in ~60 sec.

---

## Privacy posture

This is internal sales material — scores, competitor analysis, gap callouts, recommended-belt language. Not for public consumption.

- Every audit page has `<meta name="robots" content="noindex,nofollow">`
- The root `index.html` (audits list) also has noindex
- URLs are unguessable enough for casual privacy
- For real security: add Cloudflare Access (free tier, 50 users) — login-gates the whole subdomain to email addresses you approve

---

## What's NOT here

This repo only holds the **client-facing audit report HTMLs**. It does NOT hold:

- The raw scrape data (lives in each client's project folder, e.g. `C:\Users\tpete\Claude\Projects\[client]\strategy\`)
- The brand-kit / StoryBrand / execution playbook documents (same)
- The prospect's actual website code (separate per-client repo)
- Pricing, contracts, invoices (those live in GHL)

Keeping this repo tight means it stays fast and easy to navigate as the archive grows.
