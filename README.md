<p align="center"><img src="docs/assets/banner.svg" alt="CareerBridge — Experience meets ambition" width="100%" /></p>

# CareerBridge

**A mentorship marketplace that turns career goals into conversations and actionable next steps.**

[Live demo](https://careerbridge.almahfuz.chatgpt.site) · [Local setup](docs/SETUP.md) · [Architecture](docs/ARCHITECTURE.md) · [GitHub publishing](docs/GITHUB.md) · [Roadmap](docs/ROADMAP.md)

CareerBridge connects learners with working professionals and experienced mentors. It combines reviewed mentor profiles, session booking, payment workflows and an AI career studio in one workspace.

> **Status: portfolio MVP.** The source includes provider integrations, but real AI, email/SMS and gateway transactions have not been verified with live credentials. Mentor disbursement is manual. Authentication in the hosted demo is supplied by Sites; this repository is not a drop-in deployment to arbitrary hosting.

## What it does

| Area | Implemented behavior | Current boundary |
| --- | --- | --- |
| Mentor directory | Applications, admin approval, availability, fees, submitted reviews | Only real approved profiles; no fabricated ratings |
| Booking | Request, accept, decline, cancel, complete; unique slot constraint | External meeting links; no built-in video |
| AI career studio | Roadmaps, mentor matching, CV text review, five-question interviews; English/Bangla | OpenAI secret needed; mocked tests only |
| Payments | SSLCommerz checkout, verified callbacks, transaction reuse | Merchant credentials and real sandbox verification needed |
| Refunds | Eligible pre-session full refund reservation and gateway submission | Provider activation and manual status reconciliation |
| Notifications | In-app feed, Resend/Twilio adapters, SMS verification and opt-in | No unattended delivery/retry worker |
| Mentor earnings | 10% commission, seven-day hold, withdrawals and admin transfer records | Actual bank/bKash transfer remains manual |

## Stack

- **UI:** React 19, TypeScript, Lucide icons, responsive CSS.
- **Application:** Vinext (Next.js-compatible API conventions), Vite, Cloudflare Workers.
- **Data:** Cloudflare D1 / SQLite, Drizzle ORM and versioned SQL migrations.
- **Validation:** Zod, route integration tests using Node SQLite and mocked external providers.
- **Integrations:** OpenAI Responses API, SSLCommerz, Resend and Twilio.

## Engineering highlights

- Server-side authorization and per-user data access checks.
- Origin checks for authenticated write requests.
- Database constraints to prevent duplicate slots, refunds and withdrawals.
- Server-derived payment amounts and verified callback state changes.
- AI consent, opt-in profile context, bounded requests, atomic quotas and validated output.
- Mentor recommendation cards are checked against approved database IDs.
- CV text and AI conversation content are not persisted by CareerBridge.

These are implemented controls, **not a claim of a completed security audit**.

## Run and verify

Use Node 24 and the package-manager version declared in `package.json`.

```bash
npm install --global pnpm@11.25.0
pnpm install --frozen-lockfile
pnpm typecheck
pnpm test
pnpm build
```

Follow [SETUP.md](docs/SETUP.md) to initialize the local database before `pnpm dev`. Clean exports default to the portable development profile. The local development login is a simulated account, not production authentication.

## Project map

| Path | Responsibility |
| --- | --- |
| `app/page.tsx` | Marketplace, mentor, student and admin interfaces |
| `app/ai-panel.tsx` | Career studio forms, results and interview flow |
| `app/operations-panel.tsx` | Notification preferences, refunds and withdrawals |
| `app/api/` | Authenticated application and provider callback routes |
| `lib/` | Domain validation, payment/refund/delivery and AI logic |
| `db/`, `drizzle/` | Database schema and migrations |
| `tests/` | Actual route tests with SQLite and mocked providers |
| `build/`, `scripts/`, `vendor/` | Retained runtime and development support |
| `docs/` | Setup, architecture, presentation and publication guides |

## Validation and limitations

Integration suites exercise identity, origin protection, ownership, booking conflicts, gateway tampering/replay, refund uniqueness, payout eligibility, AI limits and provider failures. See [VALIDATION.md](docs/VALIDATION.md) for the export's actual checks.

Authenticated browser journeys and real provider end-to-end flows remain unverified. A CI workflow is supplied; its GitHub status is not known until it runs in the destination repository. Do not present mocked-provider results as live service verification.

## Deployment

GitHub stores and showcases this source. GitHub Pages alone cannot run its API routes or D1 database. The demo is hosted on Sites. Moving to another host requires verified authentication, provisioned storage, runtime secrets and deployment configuration. See [SETUP.md](docs/SETUP.md).

## Attribution and licensing

This project was developed with AI-assisted implementation. The runtime scaffold and third-party dependencies retain their own licensing requirements. No new open-source license is assigned in this export; choose one after reviewing ownership and upstream notices before inviting reuse. See [CONTRIBUTING.md](CONTRIBUTING.md).
