# Wentzel.ai

Solo-founder portfolio building Cytra (TRAIGA compliance), Lawvora (legal AI), Humanome (genomics), MAPS Hub (mapping), CARL (open agentic standard), OculiRX (vision care), Vector, and other products. Architectural decisions in [`wentzel/WENTZEL_PLAN.md`](https://github.com/wentzel-ai/wentzel/blob/main/WENTZEL_PLAN.md).

## CI / runner fleet

All workflows run on the self-hosted [`wentzel-runner` AWS spot fleet](https://github.com/wentzel-ai/wentzel/tree/main/tools/runner-fleet). Org policy: **never fall back to GitHub-hosted minutes**.

Two reusable workflows live in this repo at [`.github/workflows/`](.github/workflows/):

| Workflow | When | What |
|---|---|---|
| [`ci-fast.yml`](.github/workflows/ci-fast.yml) | every push + PR | prettier · eslint · tsc · vitest · build |
| [`ci-main.yml`](.github/workflows/ci-main.yml) | push to main only | playwright · lighthouse · optional deploy |

Per-repo callers are 5-10 lines each. See [`template-nextjs-saas`](https://github.com/wentzel-ai/template-nextjs-saas) for the canonical example.
