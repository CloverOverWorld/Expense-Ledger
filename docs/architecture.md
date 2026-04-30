# Ideatron Ledger — Project Architecture

**Company:** Ideatron LLC  
**Product:** Ideatron Ledger  
**Domain:** ideatron-llc.com  
**Started:** April 2026  

---

## Stack

| Layer | Service | Purpose |
|-------|---------|---------|
| DNS + CDN | Cloudflare | Domain, proxy, Zero Trust access control |
| Hosting | GitHub Pages (cloveroverworld) | Static app serving |
| Database | Supabase (free tier) | Postgres DB, auth, real-time |
| Auth | Supabase Passkeys | Face ID / Touch ID, no passwords |
| Access Control | Cloudflare Zero Trust | Email allowlist, blocks all others |

---

## Security Layers

1. **Cloudflare Zero Trust** — blocks any email not on allowlist before app loads
2. **Passkey Auth** — biometric login, no passwords stored
3. **Supabase RLS** — row level security on every table, users see only their data
4. **Encryption at rest** — Supabase encrypts all data at database level
5. **HTTPS only** — all traffic encrypted in transit

---

## Database Schema

### users
- id (uuid, primary key)
- email (text, unique)
- display_name (text)
- created_at (timestamp)

### projects
- id (uuid, primary key)
- name (text)
- owner_id (uuid, references users)
- created_at (timestamp)

### project_members
- id (uuid, primary key)
- project_id (uuid, references projects)
- user_id (uuid, references users)
- role (text: owner | editor | viewer)
- created_at (timestamp)

### expenses
- id (uuid, primary key)
- project_id (uuid, references projects)
- created_by (uuid, references users)
- date (date)
- amount (numeric)
- vendor (text)
- category (text)
- payment_method (text)
- notes (text)
- reimbursed (boolean)
- paid_by (text)
- created_at (timestamp)

### custom_categories
- id (uuid, primary key)
- project_id (uuid, references projects)
- name (text)
- created_by (uuid, references users)

---

## RLS Policies

### expenses
- SELECT: user must be a member of the expense's project
- INSERT: user must be a member of the expense's project
- UPDATE: user must be creator of the expense OR owner of the project
- DELETE: user must be creator of the expense OR owner of the project

### projects
- SELECT: user must be owner or member
- INSERT: any authenticated user
- UPDATE: owner only
- DELETE: owner only

### project_members
- SELECT: members of the same project
- INSERT: project owner only
- DELETE: project owner only

---

## Allowed Users (Cloudflare Zero Trust)

- ideatronllc@gmail.com
- srikanth.1921@gmail.com
- Beverly61200@yahoo.com

---

## Key Decisions Log

**April 2026**
- Chose plain HTML over React for portability and no-build-step deployment
- Chose Supabase over Firebase for better RLS support and Postgres familiarity
- Chose Cloudflare Zero Trust over app-level auth for domain-wide protection
- Chose passkeys over magic link for zero password friction on mobile
- Chose GitHub Pages for free static hosting with custom domain support
- Named product "Ideatron Ledger" — company brand, no separate trademark needed
- Registered agent: IncorporateMax Inc., The Woodlands TX — used as public business address

---

## Files

```
ideatron-ledger/
├── index.html        ← main app
├── privacy.html      ← privacy policy
├── terms.html        ← terms of service
└── docs/
    └── architecture.md  ← this file
```

---

## Next Steps

- [ ] Create Supabase project
- [ ] Create database tables + RLS policies
- [ ] Build app with Supabase integration
- [ ] Deploy to GitHub Pages
- [ ] Test passkey auth on iPhone + partner device
- [ ] Migrate existing expense data via CSV import
- [ ] File Ideatron trademark with USPTO (Class 36 — financial services software)
