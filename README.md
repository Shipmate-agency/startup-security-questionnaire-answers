# Startup Security Questionnaire Answers (SIG Lite / VSA Starter Pack)

Honest, copy-paste starter answers for the 18 questions enterprise buyers ask lean SaaS startups (Next.js, Supabase/Postgres, Vercel/Cloudflare, Stripe, OpenAI/Anthropic) before signing a contract.

- **Interactive builder + instant CSV/Markdown export:** https://shipmate.agency/tools/questionnaire-kit
- **Sample 1-page pentest attestation letter:** https://shipmate.agency/sample-letter
- **Pentest quote checker ($0 vs $950 vs $2,950 vs $15k):** https://shipmate.agency/tools/pentest-quote-check

## Rules before pasting into a buyer's spreadsheet
1. **Never bluff.** Only keep answers that are true for your production app today.
2. **Replace placeholders** (`[Company]`, hosting region, last pentest date).
3. **Row 14 (Pentest letter)** is the #1 deal blocker—if you have not run a test yet, send your buyer https://shipmate.agency/sample-letter first to confirm format.

## 18 Core Answers (Template)
| # | Question | Starter Answer (edit to match reality) |
|---|---|---|
| 1 | Hosting location | Application hosted on Vercel/Cloudflare (US/EU); database on managed Postgres (Supabase/RDS). |
| 2 | Encryption in transit | Yes — TLS 1.2+ enforced with HSTS; HTTP redirects to HTTPS. |
| 3 | Encryption at rest | Yes — AES-256 on database storage volumes and automated backups. |
| 4 | Multi-tenant isolation | Enforced at API and database layers (Postgres RLS / strict tenant scoping verified with two test accounts). |
| 5 | Admin MFA | Yes — MFA required on GitHub, cloud hosting, database console, and email. |
| 6 | Passwords & sessions | Salted bcrypt/Argon2 hashing via auth provider; HttpOnly/Secure session cookies. |
| 7 | Secrets management | Stored in encrypted host env vars; never committed to Git; client env vars hold public keys only. |
| 8 | Card data / PCI | No card numbers stored; Stripe (PCI-DSS Level 1) handles billing with signed webhook verification. |
| 9 | AI data training | Commercial zero-training LLM API tiers only; AI routes enforce auth, rate limits, and token caps. |
| 10 | Code review | Pull requests + automated checks before deploy; staging separated from prod secrets. |
| 11 | Dependency scanning | Continuous Dependabot / npm audit alerts; High/Critical patched on priority. |
| 12 | Security logging | Auth and access logs retained by host/DB without logging secrets or passwords. |
| 13 | Backups | Automated daily backups with tested staging restore procedures. |
| 14 | **Third-party pentest** | Manual application pentest completed on `[DATE]`; Critical/High fixed and retested. Letter attached. *(Need one fast? https://shipmate.agency/sample-letter)* |
| 15 | SOC 2 status | Early-stage company without SOC 2 Type II yet; documented controls + recent pentest letter available. |
| 16 | Breach notification | Investigated immediately; affected customers notified in writing without undue delay (≤72h where required). |
| 17 | Data deletion | Primary records deleted on request/termination; backups age out on retention schedule. |
| 18 | Subprocessors | Hosting, managed database, payment processor (Stripe), and LLM provider; list available on request. |

*Maintained by [Shipmate](https://shipmate.agency) — fixed-price security audits and 1-PR fixes for fast-built apps.*
