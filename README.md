# TedsHub

Internal training & operations portal for Ted's Hotdogs.
SOPs, 9-day new-hire training, document library, team directory,
announcements (with required-read tracking), auto-email system,
role-based admin, and more.

Single-file HTML demo (`index.html`) — no backend yet. All data is
currently stored in the browser (localStorage + IndexedDB for file
uploads). The production rollout will replace that storage layer with
Supabase + real auth, without changing the UI.

---

## Live URLs

| Environment | URL | Owner |
|-------------|-----|-------|
| Demo | `https://tedshub-demo.vercel.app` (or similar) | Mason (pre-sale) |
| Production | `https://hub.tedshotdogs.com` | Ted's Hotdogs (post-sale) |

---

## Access

Two access tiers for the demo:

| Tier | Email | PIN |
|------|-------|-----|
| Team member | `anyone@tedshotdogs.com` | `4321` |
| Admin | whitelisted `@tedshotdogs.com` | `9999` (configurable) |

Demo admin: `owner@tedshotdogs.com` / `9999`.

Admin PINs, whitelist, and email domain are all configurable from
**Settings → Admin & Security** once logged in as admin.

---

## Deployment

This repo is configured for zero-config deployment on **Vercel**.

### First-time deploy

1. Go to [vercel.com](https://vercel.com) and sign in with GitHub
2. Click **Add New → Project**
3. Select the `TedsHub` repository
4. Vercel auto-detects "Other" framework — accept defaults
5. Click **Deploy**
6. Done — site is live at `tedshub-<hash>.vercel.app`

Every `git push` to `main` automatically redeploys production. Every PR
gets its own preview URL.

### Custom domain (pre-sale)

To set up a branded pre-sale demo URL (e.g. `tedshub-demo.vercel.app`):

1. In Vercel → Project → Settings → Domains
2. Add `tedshub-demo.vercel.app`
3. Vercel handles SSL automatically

### Custom domain (post-sale, Ted's owns)

1. In Ted's DNS provider, add a `CNAME` record:
   `hub.tedshotdogs.com → cname.vercel-dns.com`
2. In Vercel → Project → Settings → Domains → Add `hub.tedshotdogs.com`
3. Vercel issues a Let's Encrypt cert in ~60 seconds

---

## Ownership & Transfer Plan

This project is structured so that **ownership can be transferred from
Mason to Ted's Hotdogs cleanly at any point** — no vendor lock-in, no
hostage data, no re-platforming.

### Current state (pre-sale)

| Asset | Owner | Transferable? |
|-------|-------|---------------|
| GitHub repo (`masonmosk/TedsHub`) | Mason | Yes — GitHub "Transfer ownership" |
| Vercel project | Mason's Vercel account | Yes — transfer to Ted's team workspace |
| Demo domain (`*.vercel.app`) | Vercel (free) | N/A (replaced at go-live) |
| Production domain (`tedshotdogs.com`) | Ted's | Already Ted's |
| Data (localStorage) | Ted's browser only | N/A — nothing server-side yet |

### Transfer workflow on contract signing

Run in this order. Each step is < 5 minutes.

1. **Ted's creates a Vercel Team workspace** (free; upgrade to Pro later
   if they want SSO / analytics)
2. **Mason transfers the Vercel project** into Ted's team:
   *Project → Settings → Advanced → Transfer*
3. **Ted's creates a GitHub org** (if they don't already have one)
4. **Mason transfers the GitHub repo** into Ted's org:
   *Repo → Settings → Danger Zone → Transfer ownership*
5. **Vercel re-connects** to the new repo location automatically
6. **Ted's IT adds the DNS CNAME** for `hub.tedshotdogs.com`
7. **Vercel adds the custom domain** and issues the cert
8. **Ted's admin email whitelist is updated** in the app Settings
9. **Mason rotates any admin PINs** from the Settings page as part of
   handoff
10. **Mason retains a collaborator seat** on the repo + Vercel project
    (defined by the support retainer) for ongoing maintenance

### What Ted's gets at handoff

- Full ownership of the code (MIT-style or custom license, TBD in contract)
- Full ownership of all hosted assets and domains
- Full ownership of all customer data
- Ability to fire the vendor (Mason) at any time and hire anyone else
  to maintain it — the whole stack is industry-standard: HTML, CSS,
  Vanilla JS today, Supabase + Vercel post-migration

---

## Roadmap

### Phase A — Polish (done)
- Icon pass (Lucide), typography, card/button polish, skeleton loaders,
  micro-animations, branded splash, mobile polish, demo banner, seeded
  realistic demo data, admin security, E2E QA.

### Phase B — Discovery & Contract (in flight)
- Scope call with Ted's COO + IT lead
- Signed proposal + 50% deposit
- Brand assets + initial user list delivered

### Phase C — Production backend (post-contract)
- Supabase project + schema
- Replace `localStorage` / `IndexedDB` with Supabase queries
- Replace browser file uploads with Supabase Storage
- Real emails via Resend (currently logs-only; EmailJS-ready alternate)
- Custom domain live

### Phase D — Microsoft integration
- Entra ID (Azure AD) OAuth → "Sign in with Microsoft"
- Group membership → role mapping
- SharePoint document library embed on the Documents page
- IT Admin role with user-management-only permissions

### Phase E — Customization & content
- Ted's brand colors, photos, logo
- Migrate real SOPs + quizzes
- Finalize email templates

### Phase F — Testing & QA, Phase G — Launch, Phase H — Post-launch
See the full checklist PDF: `TedsHub_Launch_Checklist.pdf` (on Mason's
Desktop). Roadmap lives there in detail.

---

## Local Development

```bash
# From the project root
npx serve -l 4321 .
# Then open http://localhost:4321
```

No build step. No dependencies to install. Pure static HTML.

---

## Changelog

See git history: `git log --oneline main`.

Notable tags / milestones will be added when we cut a production build.

---

## Contact

**Mason Moskowitz** — build / maintainer
(Update with phone + email once the project is formally Ted's.)
