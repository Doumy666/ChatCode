# DSH manual model catalog analysis

## Purpose

Manual, static analysis of the default-branch provider table and model catalog. It does not generate Model Watch reports, fetch live model changes, run model-watch.mjs/gen-catalog.mjs, create PRs, update seen-model state, acquire keys from tt-center, or call notification/catalog/usage backends. model-watch.yml and catalog-sync.yml are unchanged.

## Activation

After separately reviewed adoption onto the default branch, add DEEPSEEK_API_KEY as an Actions secret and manually dispatch this workflow from that default branch as Doumy666. The default-ref guard intentionally prevents running this preparation branch; no default branch was changed.

The owner guard restricts this example to Doumy666. Upstream adoption requires an explicit owner/actor policy review. Existing Actions policy may also need maintainer review to allow DSH; this change does not alter that policy. Do not make this advisory job a required replacement for existing checks.

## Pinned contract and permissions

- DSH-action v0.13.0 annotated tag was dereferenced through GitHub API to `497af93119203ca22af4f96f8fe89b3345ad665c`. The release and action.yml were checked. This verifies reference identity, not a full security audit or signature attestation.
- Exact DSH runtime: `0.2.1-rc.2`; controlled mode; Docker isolation; Worker public egress disabled.
- `allow-write: "false"`, `natural-language-write: "false"`, `task-access: read`; custom tools allow only `workspace.read` and `workspace.search`. Shell, edit, subagents and web tools are explicitly denied; no plugin installation is enabled.
- `run-tests: "false"` is intentional: the agent must not execute repository code. DSH treats this as denying mutations, not waiving write validation.
- Token permissions: contents read; no issue/PR write permission. Progress comments disabled; final review publication can still occur on PR workflows.
- Trusted-base/default checkout only, pinned checkout SHA, credentials not persisted. No PR-head checkout or repository install/build/test command is used by the agent.
- Fixed maintainer prompt: PR bodies, diffs and model output are not interpolated into action capability inputs. DSH labels fetched context as untrusted; this is a documented boundary, not proof against every prompt injection.

## Results and limitations

Inspect the DSH step summary and `result-json`, including operation, conclusion, trust, effective tools, findings and publication errors. Model output is advisory and may be wrong or incomplete. No deployment, production invocation or upstream communication is part of this integration.

No real DeepSeek call or GitHub-hosted DSH workflow run was made during preparation. Static checks cannot verify credentials, quota, Docker/image availability, model behavior, comment publication, Actions allowlists or event-time authorization. PR content is sent to DeepSeek when enabled; review that data-sharing choice before activation. A pinned Action still depends on its runtime, container, npm packages and remote API. Limits (15 minutes, 6 turns, 10 findings) can truncate analysis. Worker-network=false retains the necessary model proxy and does not make the controller offline. Review any future trusted `.dsh` Profile changes before activation.

## Official references

- [Setup and token scopes](https://github.com/Lixiaoyiao/DSH-action/blob/497af93119203ca22af4f96f8fe89b3345ad665c/docs/setup.md)
- [Action input contract](https://github.com/Lixiaoyiao/DSH-action/blob/497af93119203ca22af4f96f8fe89b3345ad665c/action.yml)
- [Security model](https://github.com/Lixiaoyiao/DSH-action/blob/497af93119203ca22af4f96f8fe89b3345ad665c/SECURITY.md)

## Upstream discussion

A narrowly scoped opt-in integration Issue is reasonable after a real maintainer-approved canary run. Present it as an optional alternative or supplement; do not claim proven security or better review quality. No Issue, PR, email or other outreach has been sent.

The official context-files contract does not accept .mjs. Only catalog/models.json is attached; the prompt requests reading sidecar/providers.mjs through the read-only workspace tool. No source file is disguised as a supported attachment type.

## Preparation validation (2026-11-11)

Passed: actionlint 1.7.12, official DSH static config checker (offline placeholder credentials only), YAML/input/SHA/permissions and unchanged-production-workflow checks. No app code changed; macOS signed packaging was not performed on this Windows host. No Model Watch scripts, notification backend, real DeepSeek API or GitHub-hosted workflow was run.
