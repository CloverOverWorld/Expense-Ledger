# Ideatron Ledger — Backlog & Tech Debt

**Last Updated:** May 2026  
**Product:** Ideatron Ledger  
**Company:** Ideatron LLC  

---

## 🔴 High Priority

| # | Item | Notes |
|---|------|-------|
| 1 | AI-assisted CSV column mapping | Requires Anthropic API key from console.anthropic.com. $5 credit covers thousands of mapping calls. Currently falls back to manual mapping. |
| 2 | Custom email with project name in invite | Supabase built-in invite email does not support dynamic project name variables. Requires Supabase Edge Function + custom SMTP to pass project name and role into email body and subject line. |

---

## 🟡 Medium Priority

| # | Item | Notes |
|---|------|-------|
| 3 | Passkey auth (Face ID / Touch ID) | Supabase passkey support is in early stages. Revisit when Supabase matures WebAuthn support. Currently using magic link which works well. |
| 4 | Import column mapping dropdown rendering | Dropdowns in AI mapping modal not rendering visibly on some screen sizes. Styling fix needed for select elements inside dynamically generated modal content. |
| 5 | Export reminder / data backup prompt | localStorage was flushed once causing data loss (pre-Supabase). Now resolved with Supabase backend, but a periodic export reminder would be good UX. |
| 6 | Supabase Vault encryption | Enable Vault for field-level encryption on sensitive expense data. Currently encrypted at rest at DB level only. |

---

## 🟢 Nice to Have / Future

| # | Item | Notes |
|---|------|-------|
| 7 | Receipt photo attachment | Allow users to attach a photo of a receipt to each expense entry. Requires Supabase Storage bucket. |
| 8 | Multi-currency support | For users tracking expenses in different currencies. Would need exchange rate API. |
| 9 | Monthly budget limits per category | Set a budget cap per category per project, show warning when approaching limit. |
| 10 | Accountant export mode | Formatted PDF or Excel export with chart of accounts, categorized by IRS Schedule C buckets. |
| 11 | Trademark filing — Ideatron Ledger | File with USPTO Class 36 (financial services software). ~$350. |
| 12 | SOC 2 compliance | Enterprise trust signal. Relevant when scaling to paying customers. ~$30-50k, not yet. |
| 13 | Google Sheets native sync | Direct read/write to a shared Google Sheet via Sheets API instead of CSV import/export. |
| 14 | Zelle/Venmo transaction auto-import | Pull transactions directly from payment apps via API or screen scrape. Reduces manual entry. |
| 15 | PWA offline mode | Cache app shell so it loads without internet. Expenses queue locally and sync when online. |
| 16 | Product Hunt launch | When feature-complete enough for public beta. |

---

## ✅ Completed

| # | Item | Completed |
|---|------|-----------|
| 1 | Basic expense entry (date, amount, vendor, category) | Apr 2026 |
| 2 | House Sale and LLC Business tabs | Apr 2026 |
| 3 | CSV export | Apr 2026 |
| 4 | CSV import with dedup logic | Apr 2026 |
| 5 | Print summary by category | Apr 2026 |
| 6 | Migrate from localStorage to Supabase | May 2026 |
| 7 | Magic link auth via Supabase | May 2026 |
| 8 | Cloudflare Zero Trust domain lockdown | May 2026 |
| 9 | Row Level Security on all tables | May 2026 |
| 10 | Real-time sync between users | May 2026 |
| 11 | Project-based expense organization | May 2026 |
| 12 | Collaborator invite system with pending invites | May 2026 |
| 13 | Role-based permissions (Owner / Editor / Viewer) | May 2026 |
| 14 | AI-assisted CSV column mapping UI (manual fallback) | May 2026 |
| 15 | Custom Supabase invite email template | May 2026 |
| 16 | Privacy policy and Terms of Service | Apr 2026 |
| 17 | Architecture documentation | Apr 2026 |
| 18 | GitHub Pages deployment at ideatron-llc.com | Apr 2026 |
| 19 | Custom domain via Cloudflare | Apr 2026 |

---

## 📝 Notes

- **Stack:** Cloudflare (DNS + Zero Trust) → GitHub Pages → Supabase (Postgres + Auth + Realtime)
- **Anthropic API key needed for:** AI CSV mapping (item #1 above)
- **Current users:** Sri (owner), Beverly (pending invite)
- **Supabase project ID:** hqnqketmvdqyldrpgbbi
- **GitHub repo:** cloveroverworld/ideatron-ledger
