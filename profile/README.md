# Wentzel.ai

Solo-operator portfolio. One human ([Ryan Wentzel](mailto:ryan@wentzel.ai)) plus AI agents — no employees, ever. ~11 products shipped across **two legal entities**, all routed through a single monorepo and a self-hosted CI fleet.

> **Brand vs legal name.** `Wentzel.ai` and `wentzel.ai` are the **brand and domain** — never a legal entity. Every contract, AWS account, Stripe account, BAA, and copyright footer uses one of the two entities below. `Wentzel.ai LLC`, `Wentzel.ai Inc`, `Wentzel AI LLC` do not exist — purge on sight.

---

## Legal entity boundary

| Entity | Jurisdiction | Owns | AWS / Stripe |
|---|---|---|---|
| **Wentzel Investments LLC** | Florida LLC | Cytra, Q, Lawvora, Humanome, MAPS Hub, CARL, Vector, CashMeUp, Nexus | Master AWS `660053610107` · existing Stripe accounts |
| **Centaris Health Inc.** | Delaware C-Corp | **[OculiRX](https://oculirx.com) — only** | **Dedicated** Centaris AWS account (first AWS Org split, FDA-triggered) · **dedicated** Centaris Stripe (creates with FDA submission) |

**OculiRX lives inside Centaris Health Inc., not Wentzel Investments LLC.** It is a Class II medical device; FDA 510(k) submission pending; pre-market promotion of a non-cleared device has FDA implications. Centaris exists so all FDA, billing, IP, and contracts for OculiRX are ring-fenced from the rest of the portfolio. Pricing publish is gated on 510(k) clearance + Centaris counsel sign-off. Operations live behind a separate Slack channel (`#oculirx-centaris`) and a separate AWS account.

---

## Products

Customer-facing brands serve from **their own apex domain**. Supporting / internal / dogfood properties live under `wentzel.ai` subdomains. Don't confuse the two — the apex is the live product; the subdomain is staging or infrastructure.

| Product | Customer URL (live) | `*.wentzel.ai` (internal/staging) | Owning entity | Repo |
|---|---|---|---|---|
| **OculiRX** *(vision care, FDA pre-submission)* | **[oculirx.com](https://oculirx.com)** | `oculirx.wentzel.ai` *(internal only)* | **Centaris Health Inc. (DE)** | [`OculiRX`](https://github.com/wentzel-ai/OculiRX) |
| Cytra *(TRAIGA / AI compliance)* | [cytra.io](https://cytra.io) | `cytra.wentzel.ai` | Wentzel Investments LLC | [`Cytra.io`](https://github.com/wentzel-ai/Cytra.io) |
| Lawvora *(legal AI)* | [lawvora.com](https://lawvora.com) | `lawvora.wentzel.ai` | Wentzel Investments LLC | [`lawvora`](https://github.com/wentzel-ai/lawvora) |
| Humanome *(genomics)* | [humanome.ai](https://humanome.ai) | `humanome.wentzel.ai` | Wentzel Investments LLC | [`humanome.ai`](https://github.com/wentzel-ai/humanome.ai) |
| MAPS Hub *(M&A excellence framework)* | [mapshub.ai](https://mapshub.ai) | `mapshub.wentzel.ai` | Wentzel Investments LLC | [`mapshub.ai`](https://github.com/wentzel-ai/mapshub.ai) |
| Vector *(Part 135 charter ops)* | [vector.wentzel.ai](https://vector.wentzel.ai) *(migrating from vector.raw-aero.com)* | — *(no separate apex — runs on subdomain)* | Wentzel Investments LLC | [`Vector`](https://github.com/wentzel-ai/Vector) |
| Q by Wentzel *(post-quantum crypto)* | [q.wentzel.ai](https://q.wentzel.ai) | — | Wentzel Investments LLC | [`quantum`](https://github.com/wentzel-ai/quantum) |
| CARL *(Code Automation Readiness Level)* | [carl.wentzel.ai](https://carl.wentzel.ai) | — | Wentzel Investments LLC | [`CARL`](https://github.com/wentzel-ai/CARL) (OSS, Apache 2.0 + CC BY 4.0) |
| CashMeUp *(SBA underwriting math)* | [cashmeup.wentzel.ai](https://cashmeup.wentzel.ai) | — | Wentzel Investments LLC | [`cashmeup`](https://github.com/wentzel-ai/cashmeup) |
| Nexus *(internal CRM + observability)* | nexus.wentzel.ai *(login wall — internal only, **never sold**)* | — | Wentzel Investments LLC | [`nexus-dashboards`](https://github.com/wentzel-ai/nexus-dashboards) |
| Wentzel.ai *(corporate site)* | [wentzel.ai](https://wentzel.ai) | — | Wentzel Investments LLC | [`wentzel.ai`](https://github.com/wentzel-ai/wentzel.ai) |
| ryanwentzel.me *(personal brand + Fractional CAIO)* | [ryanwentzel.me](https://ryanwentzel.me) | — | Ryan personal IP *(never sold with Wentzel Investments LLC)* | [`ryanwentzel.me`](https://github.com/wentzel-ai/ryanwentzel.me) |

> **Pattern, in one line:** `oculirx.com` is the product; `oculirx.wentzel.ai` is plumbing. Same pattern for `humanome.ai` vs `humanome.wentzel.ai`, `cytra.io` vs `cytra.wentzel.ai`, etc. Customer marketing, contracts, and outbound links must always use the apex.

---

## Source of truth

| Repo | What it is |
|---|---|
| **[`wentzel`](https://github.com/wentzel-ai/wentzel)** | Canonical monorepo. Master plan ([`WENTZEL_PLAN.md`](https://github.com/wentzel-ai/wentzel/blob/main/WENTZEL_PLAN.md)) + machine-readable manifest ([`WENTZEL_PLAN.lock.json`](https://github.com/wentzel-ai/wentzel/blob/main/WENTZEL_PLAN.lock.json)) + every per-product app slice under `apps/*` + shared packages under `packages/*` + IaC under `tools/*`. Read `WENTZEL_PLAN.md` first for any architectural question. |
| **[`CARL`](https://github.com/wentzel-ai/CARL)** | Open standard — Code Automation Readiness Level spec + assessor + reference prompts (Apache 2.0 + CC BY 4.0). Community comments via [carl.wentzel.ai/comments](https://carl.wentzel.ai/comments), not GitHub Issues. |
| **[`.github`](https://github.com/wentzel-ai/.github)** | This repo — org-level shared GitHub config, reusable workflows, and the org profile you're reading. |

---

## CI / runner fleet

All workflows run on the self-hosted [`wentzel-runner` AWS spot fleet](https://github.com/wentzel-ai/wentzel/tree/main/tools/runner-fleet) — philips-labs `terraform-aws-github-runner` v6, ephemeral c7g.large arm64 Graviton spot. **Org policy: never fall back to GitHub-hosted minutes.**

Two reusable workflows live here at [`.github/workflows/`](.github/workflows/):

| Workflow | When | What |
|---|---|---|
| [`ci-fast.yml`](.github/workflows/ci-fast.yml) | every push + PR | prettier · eslint · tsc · vitest · build |
| [`ci-main.yml`](.github/workflows/ci-main.yml) | push to main only | playwright · lighthouse · optional deploy |

Per-repo callers are 5–10 lines each. Canonical example: [`template-nextjs-saas`](https://github.com/wentzel-ai/template-nextjs-saas).

---

## Security

Vulnerability disclosures → **security@wentzel.ai** · 24-hour acknowledgement target · `/.well-known/security.txt` per RFC 9116 on every product apex.

OculiRX security disclosures may also be routed via Centaris Health Inc. once the FDA submission goes in — same inbox until further notice.

---

## Contact

**Owner:** Ryan Wentzel · [ryan@wentzel.ai](mailto:ryan@wentzel.ai) · [ryanwentzel.me](https://ryanwentzel.me)

External contributions are **not** accepted on portfolio repos. The CARL standard accepts community input via [carl.wentzel.ai/comments](https://carl.wentzel.ai/comments).
