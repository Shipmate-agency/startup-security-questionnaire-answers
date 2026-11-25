<p align="center">
  <a href="https://shipmate.agency/tools/questionnaire-kit">
    <img src="./assets/banner.png" alt="Startup Security Questionnaire Answers (SIG Lite / VSA) by Shipmate" width="840" />
  </a>
</p>

# Startup Security Questionnaire Answers (SIG Lite / VSA Starter Pack)

[![Interactive Builder](https://img.shields.io/badge/Interactive_CSV_Builder-shipmate.agency-1E57A8?style=flat-square)](https://shipmate.agency/tools/questionnaire-kit)
[![Sample Pentest Letter](https://img.shields.io/badge/Sample_Pentest_Letter-View-11141C?style=flat-square)](https://shipmate.agency/sample-letter)
[![License: MIT](https://img.shields.io/badge/License-MIT-11141C?style=flat-square)](./LICENSE)

Honest, non-bluffing starter answers to the **18 enterprise security questionnaire questions** (topics common to SIG Lite / VSA / CAIQ) often sent to lean SaaS teams running **Next.js, Supabase/Postgres, Vercel/Cloudflare, Stripe, and OpenAI/Anthropic**.

- **Customize with your stack & export CSV/Markdown:** https://shipmate.agency/tools/questionnaire-kit
- **Got hit with Row #14 (Pentest Letter)?** Inspect the public format first: https://shipmate.agency/sample-letter

## Rules Before Pasting Into a Buyer's Spreadsheet
1. **Never overclaim.** Keep only answers that accurately reflect your production system today. If a row is not true yet, answer "No" or "Planned for [date]". A wrong "Yes" can become a contract misrepresentation.
2. **Your vendors' certifications are not yours.** Vercel, Supabase and Stripe hold their own SOC 2 / ISO 27001 / PCI DSS attestations. They cover the vendor's platform, not your company or your code. Say "our hosting provider is SOC 2 Type 2", never "we are SOC 2 compliant".
3. **Customize placeholders** (`[Company]`, `[region]`, `[N days]`, `[DATE]`). Bracketed text is an example, not a fact about you.
4. **Unblock Row #14 fast:** If you don't have a third-party pentest letter yet, check whether your buyer accepts [Shipmate's 1-page attestation letter](https://shipmate.agency/sample-letter) (`$2,950 once`, target 5 business days).

## 18 Core Starter Answers
Questions are paraphrased, not copied from any questionnaire. The CAIQ column gives the [CSA Cloud Controls Matrix v4](https://cloudsecurityalliance.org/research/cloud-controls-matrix) domain where the topic usually appears; SIG Lite and VSA ask about the same topics under their own section names.

| # | Category | CAIQ domain | Question | Starter Answer (verify before sending) |
|---:|---|---|---|---|
| 1 | Hosting | DSP | Where is data hosted? | Web app on [Vercel/Cloudflare]; application data in managed Postgres ([Supabase/RDS]) in [region, e.g. AWS eu-central-1]. |
| 2 | Transit | CEK | Encrypted in transit? | Yes. All endpoints are HTTPS-only (TLS 1.2 or newer); plain HTTP redirects to HTTPS; HSTS is set on [domains]. |
| 3 | Rest | CEK | Encrypted at rest? | Yes. Our database provider encrypts data and backups at rest with AES-256 using provider-managed keys. |
| 4 | Isolation | AIS | Multi-tenant separation? | Every query is scoped to the signed-in tenant at the API and database layer (Postgres RLS / tenant ID checks), last tested with two separate accounts on [DATE]. |
| 5 | Access | IAM | Admin MFA? | Yes. MFA is enforced for everyone with access to GitHub, hosting, the database console, and email. |
| 6 | Auth | IAM | Passwords & sessions? | Passwords are hashed by our auth provider ([Supabase Auth: bcrypt]); we never store plaintext. Sessions use short-lived access tokens with refresh tokens, sent over HTTPS only. |
| 7 | Secrets | CEK | Secrets management? | Stored in our host's environment variables, which are encrypted at rest; never committed to Git; browser code only receives publishable keys. |
| 8 | Payments | DSP | Card storage / PCI? | We do not store, process or transmit card numbers; Stripe collects card data via [Checkout/Elements]. Stripe is a PCI DSS Level 1 Service Provider. We complete our own PCI self-assessment ([SAQ A]). Webhooks verify Stripe's signature. |
| 9 | AI / LLMs | STA | Model training on data? | We use [OpenAI API / Anthropic API] under commercial terms, which state API data is not used for training by default. The provider may keep data for [N days] for abuse monitoring. AI routes require login, rate limits, and token caps. |
| 10 | SDLC | CCC | Code review? | Every change goes through a pull request with automated security checks before deploy; staging is separate from production. |
| 11 | Packages | TVM | Dependency CVEs? | Dependabot / `npm audit` alerts on vulnerable packages; High/Critical patched within [N days]. |
| 12 | Logging | LOG | Security logging? | Auth events, access errors and app logs are kept by our providers for [N days]; we never log passwords or secrets. |
| 13 | Backups | BCR | Backup cadence? | Daily automated backups by [Supabase Pro / RDS], kept [7] days. Last restore test: [DATE]. |
| 14 | **Pentest** | TVM | **Third-party pentest letter?** | Manual web app pentest by [firm] completed on `[DATE]`; Critical/High fixed and retested. Letter attached. *([Need one fast?](https://shipmate.agency/sample-letter))* |
| 15 | SOC 2 | A&A | Current SOC 2 Type II? | No, not yet. Our infrastructure providers ([Vercel, Supabase, Stripe]) have their own SOC 2 reports covering their platforms. We can share [our written security policies] and a recent pentest letter. |
| 16 | Incidents | SEF | Breach notice SLA? | Investigated on detection; affected customers notified in writing without undue delay and within [72 hours / the period in our contract or DPA], plus any notice required by law. |
| 17 | Deletion | DSP | Data deletion on exit? | Primary records deleted within [N days] of a written request or contract end; backups expire on the provider's schedule ([7] days). |
| 18 | Vendors | STA | Subprocessor list? | Hosting, managed database, Stripe, and LLM provider; current list available on request. |

## What to Check Before Each "Yes"
Do not send a row unless you can show it is true. Vendor facts below were checked against the vendors' public pages on 2026-11-24; re-check them, since plans and terms change.

| Row | Check this yourself | Vendor facts (source) |
|---:|---|---|
| 1 | Region of your database project and your function region. | Vercel functions run in the region you choose ([Vercel compliance](https://vercel.com/docs/security/compliance)). |
| 2 | Run your domain through [MDN HTTP Observatory](https://developer.mozilla.org/en-US/observatory) to confirm the HTTPS redirect and HSTS header. | Vercel and Supabase encrypt traffic with TLS ([Vercel](https://vercel.com/docs/security/compliance), [Supabase](https://supabase.com/security)). |
| 3 | That every datastore (database, file storage, logs, analytics) is with a provider that encrypts at rest. | Supabase: AES-256 at rest ([security](https://supabase.com/security)). Vercel: AES-256 at rest ([compliance](https://vercel.com/docs/security/compliance)). |
| 4 | Only claim the two-account test if you ran it and every customer table has RLS or an equivalent check. | - |
| 5 | MFA is enforced in each org's settings, not just enabled by some people. | - |
| 6 | How your app stores sessions. Do not claim HttpOnly cookies on a default Supabase setup: its SSR cookies are readable by browser code by design ([Supabase](https://supabase.com/docs/guides/auth/server-side/advanced-guide)). | Supabase Auth hashes passwords with bcrypt ([password security](https://supabase.com/docs/guides/auth/password-security)). |
| 7 | No secret in `NEXT_PUBLIC_` / `VITE_` variables or Git history. | Vercel environment variables are encrypted at rest ([docs](https://vercel.com/docs/environment-variables)). |
| 8 | Your SAQ type in the Stripe Dashboard. Using Stripe does not make you PCI compliant; you still validate your own compliance. | Stripe: PCI Service Provider Level 1 ([security](https://docs.stripe.com/security)). |
| 9 | Your provider, plan, any zero-data-retention agreement, and that no feedback/opt-in setting shares data for training. | OpenAI: no training on business/API data by default ([enterprise privacy](https://openai.com/enterprise-privacy/)). Anthropic: no training on commercial/API data by default ([privacy center](https://privacy.claude.com/en/articles/7996868-is-my-data-used-for-model-training)). |
| 10 | Branch protection actually requires a reviewed PR. A solo founder should say "self-reviewed with automated checks". | - |
| 12 | Your plan's log retention; buyers often expect 90 days or more, which needs log drains or a paid tier. | Supabase API/DB logs: Free 1 day, Pro 7, Team 28, Enterprise 90 ([logs](https://supabase.com/docs/guides/observability/logs)). Vercel runtime logs: Hobby 1 hour, Pro 1 day, Enterprise 3 days, 30 days with Observability Plus ([logs](https://vercel.com/docs/logs/runtime)). |
| 13 | Your plan includes backups and when you last restored one. | Supabase backs up Pro, Team and Enterprise projects daily (7/14/30 days kept); Free projects get no automatic backups, and backups do not include Storage objects ([backups](https://supabase.com/docs/guides/platform/backups)). |
| 14 | You have a signed letter from the firm that tested you. Never write or edit the letter yourself. | - |
| 15 | Which written policies you really have. Vendor SOC 2 reports usually need an NDA to share and describe the vendor only. | Vercel: SOC 2 Type 2, ISO 27001:2022, PCI DSS AOC ([compliance](https://vercel.com/docs/security/compliance)). Supabase: SOC 2 Type 2, ISO 27001 ([security](https://supabase.com/security)). |
| 16 | The notice period in your signed contracts and DPA, and the laws that apply to your users. | - |
| 17 | You can actually delete a customer's rows, files and logs on request. | - |

Part of **[Shipmate Open Source](https://github.com/Shipmate-agency)** · [`pentest-attestation-letter-template`](https://github.com/Shipmate-agency/pentest-attestation-letter-template) · [shipmate.agency](https://shipmate.agency)
