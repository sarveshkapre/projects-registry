# projects

## Strategy (continuous)
- This file is the project registry. Each row = one repo = one shippable product.
- Before starting any row: check my GitHub/local clones; if it exists, iterate/improve it (no duplicates).
- Every repo must be production-ready: standard scaffolding docs/files (README/AGENTS/PLAN/PROJECT/CHANGELOG/ROADMAP/RELEASE/SECURITY/CONTRIBUTING/CODE_OF_CONDUCT/LICENSE/.gitignore), CI, Docker (or explicit N/A), safe defaults, no secrets.
- Quality gate: `make/just check` must pass locally and in CI before moving to the next project.
- UX bar: minimalist, fast, responsive, dark mode, keyboard-first, accessible.
- Security bar: input validation, least privilege, secret scanning, dependency/SAST checks, threat-model notes.
- Iteration: keep polishing after v0.1.0; update status here + keep CHANGELOG as the source of “what shipped”.

## Build contract (continuous)
- No authentication yet. Ship products that are fully functional without accounts: single-user, local-first, or “open access” modes only.
- Every project is a public GitHub repo (no private repos by default).

### Standard repo scaffolding (must exist before coding)
- Ensure the project directory exists (create if missing).
- Initialize git, add `.gitignore`, `LICENSE`, and basic repo hygiene files.
- Required docs/files (always present):
  - `README.md` (what it is, screenshots/GIFs if UI, quickstart)
  - `AGENTS.md` (how to work in this repo; guardrails; commands; conventions)
  - `PLAN.md` (architecture + milestones + MVP checklist + risks)
  - `PROJECT.md` (exact commands: setup/dev/test/lint/typecheck/build/release)
  - `CHANGELOG.md`, `ROADMAP.md`, `RELEASE.md`, `SECURITY.md`
  - `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`
  - Except for `README.md` put all other .md files in one folder
- Required engineering:
  - CI (lint + tests + build) on every push/PR
  - Docker support (or explicit “not applicable” note in README)
  - Secret scanning + dependency/SAST checks in CI (with sane defaults)
  - A single quality gate command: `make check` or `just check`
  - A `Makefile` or `justfile` with at least: `setup`, `dev`, `test`, `lint`, `typecheck`, `build`, `check`, `release`

### Development workflow (always)
- Start with planning: write `PLAN.md` first, then scaffold, then implement.
- Work in small steps:
  - implement a feature slice
  - update tests
  - update docs if behavior changed
  - update `CHANGELOG.md` for shipped user-facing changes
- After every meaningful feature/change: commit + push to GitHub (keep main branch green).
- Do not fabricate history: commits and changelog entries must match what actually changed.

## PLAN.md — Codex execution contract (continuous)
This is the operating procedure for turning `projects.md` rows into public, production-grade repos.

1. Source of truth: `projects.md`. For each row, first check local clones and GitHub under the target owner/org. If the repo exists: improve it (preferred) or skip if it already meets the contract. Never create duplicates.
2. Stack selection: choose the smallest, most maintainable stack that fits the pitch.
   - Prefer boring defaults and strong tooling.
   - Document the chosen stack + rationale in `PLAN.md`.
   - Pin versions (toolchain + deps) and ensure reproducible builds.
3. Required repo files (always present):
   - `README.md`
   - `AGENTS.md`
   - `PLAN.md`
   - `PROJECT.md` (exact commands and workflows)
   - `CHANGELOG.md`
   - `ROADMAP.md`
   - `RELEASE.md`
   - `SECURITY.md`
   - `LICENSE`
   - `CONTRIBUTING.md`
   - `CODE_OF_CONDUCT.md`
   - `.gitignore`
4. Scope discipline: each repo ships one clear use-case, runnable end-to-end, with tight MVP scope. Non-goals and next steps must be explicit in `ROADMAP.md`.
5. One-command workflows: provide `Makefile` or `justfile` with at least:
   - `setup`, `dev`, `test`, `lint`, `typecheck`, `build`, `check`, `release`
   - `check` must be the canonical gate (aggregates tests + lint + typecheck + build).
6. UX bar (if UI exists): minimalist, fast, responsive, keyboard-first, dark mode, and accessible (a11y). Keep UI dependency footprint small.
7. Security bar (always):
   - Never commit secrets. Include secret-scanning guidance and local `.env` patterns.
   - Safe-by-default configs; strict input validation.
   - Add guardrails relevant to the project (e.g., SSRF/XSS/IDOR where applicable).
   - Least privilege for any credentials, tokens, or permissions.
8. Quality gates (mandatory):
   - Unit tests + at least one integration/smoke test where meaningful.
   - Lint/format, type-check (when language supports it), build step.
   - Deterministic outputs and pinned tooling versions.
9. CI (mandatory): GitHub Actions must run `check` on pushes/PRs. Add dependency scanning and lightweight SAST where reasonable. No green CI = not done.
10. Iteration loop per repo:
   - Plan → scaffold → implement smallest slice → run `check` locally → fix until green
   - One refactor pass (clarity/structure)
   - One UX polish pass (if UI)
   - One security hardening pass
   - Re-run `check` and ensure CI is green
11. Documentation standard (minimal but sufficient):
   - Short architecture note (and diagram if helpful)
   - Threat-model notes (key risks + mitigations)
   - Known limitations
   - “Next 3 improvements” list (in `PROJECT.md` or `ROADMAP.md`)
12. Release discipline:
   - Update `CHANGELOG.md` with shipped user-facing changes.
   - Follow SemVer (pre-1.0 allowed).
   - Cut `v0.1.0` when MVP is real and `check` + CI are green.
   - Publish a GitHub Release and link it back in `projects.md` (status + URL).

## Status legend
- backlog | scaffolded | mvp | hardened | shipped

## Row template
| Project name | Repo name | Pitch | Status |
|---|---|---|---|
| Name | repo-slug | One sentence: what + for whom + why it matters | backlog |

---

## Security & AppSec tools (28)
| Project name | Repo name | Pitch | Status |
|---|---|---|---|
| JWT Workbench | jwt-workbench | jwt.io-style offline JWT decode/verify/sign + JWK/JWKS tools + common footgun checks | shipped (v0.1.0: https://github.com/sarveshkapre/jwt-workbench/releases/tag/v0.1.0) |
| WebProxy Suite | webproxy-suite | Burp-style intercepting proxy + repeater + safe scanner + reproducible test artifacts | shipped (v0.1.0: https://github.com/sarveshkapre/webproxy-suite/releases/tag/v0.1.0) |
| SSRF Sentinel | ssrf-sentinel | SSRF scanner + safe PoC harness with strict redirect/DNS/IP controls and evidence output | shipped (v0.1.0: https://github.com/sarveshkapre/ssrf-sentinel/releases/tag/v0.1.0) |
| IDOR Lens | idor-lens | IDOR detector via role/token differential testing + minimal proof + regression mode | shipped (v0.1.0: https://github.com/sarveshkapre/idor-lens/releases/tag/v0.1.0) |
| Subdomain Scout | subdomain-scout | Subdomain discovery (CT/DNS/wordlists) + diffs + takeover signals + risk scoring | shipped (v0.1.0: https://github.com/sarveshkapre/subdomain-scout/releases/tag/v0.1.0) |
| PCAP Inspector | pcap-inspector | PCAP analyzer that builds a flow timeline + extracts DNS/HTTP/TLS metadata + exports | shipped (v0.1.0: https://github.com/sarveshkapre/pcap-inspector/releases/tag/v0.1.0) |
| File Sanitizer | file-sanitizer | Upload files, sanitize contents (metadata/macros/scripts), and re-export safely with logs | shipped (v0.1.0: https://github.com/sarveshkapre/file-sanitizer/releases/tag/v0.1.0) |
| Log Redactor | log-redactor | Redact secrets/PII from logs with configurable rules, tests, and safe defaults | shipped (v0.1.0: https://github.com/sarveshkapre/log-redactor/releases/tag/v0.1.0) |
| Secret Scanner Plus | secret-scanner-plus | Repo secret scanning (entropy+regex+history) with remediation guidance and CI gate | shipped (v0.1.0: https://github.com/sarveshkapre/secret-scanner-plus/releases/tag/v0.1.0) |
| SBOM Forge | sbom-forge | Generate SBOM (SPDX/CycloneDX) + license report + diffs per release | backlog |
| Dependency Risk Dashboard | dependency-risk-dashboard | UI for CVE/license risk + upgrade recommendations + exportable evidence | backlog |
| CVE Risk MCP Server | cve-risk-mcp | MCP server for CVE lookup + EPSS-style risk scoring + “what should I patch first?” queries | backlog (P0) |
| OpenAPI Fuzzer | openapi-fuzzer | Safe fuzzing from OpenAPI specs with repro bundles and CI mode | scaffolded |
| GraphQL Guard | graphql-guard | GraphQL security checks (auth gaps, depth/cost, introspection exposure) with reports | backlog |
| CSP Doctor | csp-doctor | Analyze CSP and generate a safe rollout plan + report-only config generator | scaffolded |
| Header Shield | header-shield | Security headers linter + nginx/caddy templates + CI gate | backlog |
| OAuth Flow Lab | oauth-flow-lab | OAuth/OIDC test bench (PKCE, device flow, token exchange) with replayable traces | backlog |
| SAML Inspector | saml-inspector | Parse/validate SAML assertions and signatures; common misconfig checks | backlog |
| Webhook Sentry | webhook-sentry | Verify webhook signatures + replay protection; generate fixtures and test vectors | backlog |
| Session Cookie Lab | session-cookie-lab | Session/cookie analyzer: SameSite, secure flags, rotation, fixation tests | backlog |
| TLS Inspector | tls-inspector | TLS/cert scanner with actionable remediation and CI mode | backlog |
| DNS Posture Scanner | dns-posture-scanner | SPF/DMARC/DKIM checks + dangling record/takeover signals + reporting | backlog |
| Safe Fetcher | safe-fetcher | Hardened URL fetcher library (SSRF-safe, allowlists, caps, redirect policy) | backlog |
| Webhook Replay Studio | webhook-replay-studio | Record/replay webhooks locally with diff, filters, and shareable bundles | backlog |
| API Auth Diff | api-auth-diff | Compare endpoint behavior across roles/tokens to surface authZ regressions | backlog |
| Disclosure Kit | disclosure-kit | Generator for SECURITY.md + security.txt + disclosure workflows | backlog |
| Secure Defaults Linter | secure-defaults-linter | Lint configs for unsafe defaults and propose patches with tests | backlog |

---

## Enterprise BAS / control validation (6)
| Project name | Repo name | Pitch | Status |
|---|---|---|---|
| BAS Orchestrator | bas-orchestrator | SafeBreach-style campaign engine + distributed agents + scoring + evidence pack | scaffolded (P0) |
| BAS Agent | bas-agent | Endpoint agent to execute safe “attack modules” with strict scoping + telemetry | backlog |
| Attack Module SDK | bas-module-sdk | Spec/SDK to author atomic safe behaviors with prerequisites + evidence outputs | backlog |
| Safe Canary Kit | safe-canary-kit | Canary secrets/artifacts + validators so modules are machine-verifiable | backlog |
| Detection Matcher | detection-matcher | Match expected detections vs SIEM/EDR logs and produce gap + fix recommendations | backlog |
| Control Coverage Console | control-coverage-console | SOC-console UI: dashboards, heatmap, findings backlog, exports | backlog |

---

## LLM / agents / agent security (23)
| Project name | Repo name | Pitch | Status |
|---|---|---|---|
| Agent Swarm Control Panel | agent-swarm-control-panel | One UI to run multiple agents (researcher/coder/tester/writer/scheduler) with approvals + logs | mvp |
| LLM Agent Playground | llm-agent-playground | Call different LLMs, compare responses, costs, tool use, and eval scores | mvp |
| Agentic Writing IDE | agentic-writing-ide | Document-first writing IDE for blog posts: multi-agent draft→critique→revise→polish with commit/diff/branch history and rationale | scaffolded |
| Prompt Injection Firewall | prompt-injection-firewall | Reverse proxy that gates model + tools with allow/deny/approve rules and full audit trace | shipped (v0.1.1: https://github.com/sarveshkapre/prompt-injection-firewall/releases/tag/v0.1.1) |
| MCP Proxy Gateway | mcp-proxy-gateway | Observe/gate MCP tool calls with schema validation + record/replay for deterministic tests | shipped (v0.1.0: https://github.com/sarveshkapre/mcp-proxy-gateway/releases/tag/v0.1.0) |
| Agent Security CI | agent-security-ci | “Agent security BAS”: scenario DSL + regressions + CI/nightly scorecards | backlog (P0) |
| Toolcall Simulator | toolcall-simulator | Mock MCP tools (files/chat/docs/git/etc) to test agents safely and deterministically | backlog |
| Context Compiler | context-compiler | “Untrusted text quarantine” compiler for RAG prompts with deterministic assembly | backlog |
| Output DLP Guard | output-dlp-guard | Post-generation leak guard: secrets/PII/high-entropy/verbatim detection + redaction | backlog |
| RAG Sanitizer | rag-sanitizer | Strip instruction-like retrieval content, risk score chunks, enforce citations | backlog (P0) |
| Retrieval Boundary Enforcer | retrieval-boundary-enforcer | Permission-aware retrieval + provenance mapping so agents can’t cross boundaries | backlog |
| Canary Secrets Detector | canary-secrets-detector | Detect canary exfil and show exact leak path in traces | backlog |
| Eval Harness Core | eval-harness-core | Define tasks/rubrics, run evals, regression gate, publish reports | backlog |
| Prompt Mutation Lab | prompt-mutation-lab | Mutate prompts automatically and keep best versions by eval score | backlog |
| Judge Calibrator | judge-calibrator | Calibrate judge models/prompts; measure bias/variance and stabilize scoring | backlog |
| Multi-Agent Toybox | multi-agent-toybox | Coordinator/worker patterns with measurable success metrics and reproducible runs | backlog |
| Agent Recorder | agent-recorder | Record every tool call + output; replay deterministically for debugging and regressions | backlog |
| Agent Trace Viewer | agent-trace-viewer | Flight-recorder UI for tool chains, decisions, failures, and leak-path highlights | backlog |
| LLM Social Sandbox | llm-social-sandbox | “AI social feed” to test moderation/ranking, safety knobs, and evaluation metrics | backlog |
| Local Model Bench | local-model-bench | Benchmark on-device LLMs (latency/quality) with standardized tasks + reports | backlog |
| DevTools Copilot | devtools-copilot | Chrome DevTools monitor that explains network/perf/errors and suggests fixes | backlog |
| DevTools Request Shield | devtools-request-shield | DevTools UI that flags/blocks insecure requests and highlights risky patterns | backlog (P0) |
| Prompt Pack Registry | prompt-pack-registry | Versioned prompt packs with tests and safety regressions (like “prompts as code”) | backlog |

---

## Devtools / DX / utilities (26)
| Project name | Repo name | Pitch | Status |
|---|---|---|---|
| HTTP Playground | http-playground | Postman-like client with OAuth helpers, replay, diff, and shareable collections | backlog (P0) |
| AI Mermaid Live Editor | ai-mermaid-live-editor | Split-screen Mermaid editor + live renderer + AI chat that generates/refactors diagrams via patches; commit history, diffs, export/share | mvp |
| Regex Explainer | regex-explainer | Regex playground: explain, generate tests, visualize groups, warn on perf traps | backlog |
| Cron Visualizer | cron-visualizer | Human ↔ cron translator with next-run simulation across timezones | backlog |
| Diff to PR Summary | diff-to-pr-summary | Paste a git diff → PR summary, risk assessment, and suggested test plan | backlog |
| JSON Schema Studio | json-schema-studio | JSON→schema, docs, validators, sample generator, and diff tool | backlog |
| API Contract Tester | api-contract-tester | Backward compatibility checks for OpenAPI/JSON schema in CI | backlog |
| OpenAPI Doc Portal | openapi-doc-portal | Beautiful API docs site with runnable examples and code snippets | backlog |
| DevEx Agent | devex-agent | Dev advocate assistant that turns OpenAPI specs into API docs with examples and auto-regenerates on change | mvp (repo: https://github.com/sarveshkapre/devex-agent) |
| API Mock Server | api-mock-server | Mock APIs from OpenAPI + record/replay fixtures deterministically | backlog |
| CLI TUI Starter | cli-tui-starter | Beautiful minimal TUI template with commands, themes, and accessibility | scaffolded (P0) |
| Repo Scaffolder | repo-scaffolder | Generates repos from your golden template and auto-updates this projects.md | shipped (v0.1.0: https://github.com/sarveshkapre/repo-scaffolder/releases/tag/v0.1.0) |
| Write for Humans + AIs | write-for-humans-ais | Publishing layer that generates AI-canonical artifacts (/llms.txt, /llms-full.txt, clean per-URL markdown w/ stable anchors, JSON-LD, claims/glossary metadata, content-addressed builds) and runs a continuous “AI comprehension fidelity” eval harness (retrieval-only answers w/ citations, score correctness/coverage/ambiguity/compression, produce fix recommendations) | scaffolded (P0): https://github.com/sarveshkapre/write-for-humans-ais |
| EmbedDB | embeddb | Rust single-node embedded DB (WAL+LSM: memtable→SST+compaction) with tables of typed rows and automatic per-row embeddings on insert/update (commit primary write durably first, then enqueue idempotent embedding jobs with status pending/ready/failed + hash); vector kNN search (cosine/L2; brute-force MVP → HNSW V1); pluggable local-first embedder + optional remote feature flag; observability + crash-recovery tests; embedded lib + optional server/CLI | mvp |
| GitHub Project Pilot | github-project-pilot | Backlog → plans → GitHub repos/issues/PRs with an AI orchestrator that drives real shipping without fabricating history; optional local “simulated timeline” | mvp (P0) |
| Release Notes Writer | release-notes-writer | CHANGELOG/commits → curated RELEASE.md notes with links and highlights | backlog |
| Status Page Lite | status-page-lite | Self-hosted status page + incident updates + RSS + exportable history | backlog |
| Error Tracker Lite | error-tracker-lite | Lightweight self-hosted error tracking with grouping and alerts | backlog |
| Uptime Monitor Lite | uptime-monitor-lite | Uptime checks, alerting, SLA reports, and incident history | backlog |
| Privacy Analytics Lite | privacy-analytics-lite | Cookie-less analytics dashboard with exports and privacy-first defaults | backlog |
| Scheduling Link Lite | scheduling-link-lite | Booking links + availability rules + calendar sync (self-hostable) | backlog |
| Codebase Explainer | codebase-explainer | Repo → architecture map + dependency graph + Q&A with citations to files | backlog |
| Dev Environment Hub | dev-environment-hub | Coder-like self-hosted remote dev workspaces for teams | backlog |
| Screenshot Diff Tool | screenshot-diff-tool | Visual regression testing with fast diffs and CI artifacts | backlog |
| Markdown to Slides | markdown-to-slides | Turn markdown into polished slides with a minimal theme and export | backlog |
| API Timeline Profiler | api-timeline-profiler | Trace local API calls; generate waterfall timelines + perf hints | backlog |
| IIT Exam Evals | iit-exam-evals | IIT-style evaluation engine with rubrics, grading, and analytics (offline mode) | backlog |

---

## UI / design systems (7)
| Project name | Repo name | Pitch | Status |
|---|---|---|---|
| Liquid Glass UI | liquid-glass-ui | Apple liquid-glass style component site + tokens + a11y + dark mode | backlog (P0) |
| Design Token Pipeline | design-token-pipeline | Versioned design tokens → CSS/TS exports + diffs and release flow | backlog |
| Motion Microinteractions | motion-microinteractions | Tasteful motion primitives with reduced-motion support and docs | backlog |
| Layout Primitives | layout-primitives | Stack/grid/container primitives with consistent spacing rules and a11y | backlog |
| Theme Builder | theme-builder | Generate color systems with contrast checks and dark-mode pairing | backlog |
| Screenshot to Component | screenshot-to-component | Turn screenshots into reusable components + tests (design-to-code helper) | backlog |
| App Shell Starter | app-shell-starter | Production-ready app shell: auth, settings, a11y, dark mode, perf budget | backlog |

---

## Endpoint / ops (8)
| Project name | Repo name | Pitch | Status |
|---|---|---|---|
| FleetMDM | fleet-mdm | Jamf-like management for macOS + Linux: inventory, policies, scripts, compliance | backlog (P0) |
| Endpoint Perf Agent | endpoint-perf-agent | Cross-platform endpoint performance agent with anomaly detection + explainers | scaffolded (repo: https://github.com/sarveshkapre/endpoint-perf-agent) |
| On-Device Guard | on-device-guard | On-device LLM to summarize suspicious processes/network behavior and create reports | backlog (P0) |
| Process Telemetry Collector | process-telemetry-collector | Collect process/file/network events (best-effort cross-platform) for analysis | backlog |
| Patch Compliance Dashboard | patch-compliance-dashboard | Track OS/package patch state; export evidence; scheduled reports | backlog |
| Secure Baseline Enforcer | secure-baseline-enforcer | Apply hardened baselines with dry-run, rollback, and audit logs | backlog |
| Zero Trust Tunnel Lite | zero-trust-tunnel-lite | mTLS tunnel + policy allowlists for self-hosted services | backlog |
| Secretive-X | secretive-x | Secretive for Windows/Linux/macOS: non-exportable SSH keys via Secure Enclave/FIDO2/TPM | mvp |

---

## Workspaces / collaboration (6)
| Project name | Repo name | Pitch | Status |
|---|---|---|---|
| eSign + Document Chat | esign-document-chat | Distinct DocuSign-like e-sign (PDF upload→draggable fields: signature/initials/date/name/text/checkbox→recipient routing seq/parallel→secure expiring links + reminders/void; status timeline; signing ceremony w/ adopt signature + consent capture; tamper-evident hash + signed PDF + completion certificate/audit trail + export/API) plus “Ask this document” chat with viewer highlights, page+snippet citations, clause extraction, and risk flags (informational only; not legal advice) | scaffolded |
| Collaborative Design Canvas | collaborative-design-canvas | Distinct Figma-inspired collaborative canvas MVP: infinite canvas w/ frames/artboards; shapes/text/images; pages+layers tree; properties panel; pan/zoom; selection+transforms; undo/redo; autosave; export PNG/SVG + JSON; real-time multiplayer (presence/cursors/live edits) with CRDT merges; optional pinned comment threads | mvp |
| Sketchboard Chat | sketchboard-chat | Excalidraw clone with realtime chat + multiplayer presence and exports | backlog (P0) |
| Slack Workspace Synth | slack-workspace-synth | Create a 2000-person synthetic Slack workspace + messages/files via a plug-in API | mvp (v0.1.0: https://github.com/sarveshkapre/slack-workspace-synth/releases/tag/v0.1.0) |
| Google Workspace Synth | google-workspace-synth | Synthetic Google Workspace (Docs/Drive/Sheets) with permissions + sharing APIs | mvp |
| Notion Workspace Synth | notion-workspace-synth | Synthetic Notion-like pages/databases/comments API + seeded demo org | shipped (v0.1.0: https://github.com/sarveshkapre/notion-workspace-synth/releases/tag/v0.1.0) |

---

## Photo / media (3)
| Project name | Repo name | Pitch | Status |
|---|---|---|---|
| AI Headshot Studio | ai-headshot-studio | Headshot generator + background removal + lighting/retouch + crop presets | mvp |
| Passport/Visa Photo Fixer | passport-photo-fixer | Passport/visa photo fixer with strict compliance checks + printable sheets | backlog (P0) |
| Image Privacy Scrubber | image-privacy-scrubber | Batch remove EXIF, blur faces/plates, watermark, resize; local-first processing | backlog |
