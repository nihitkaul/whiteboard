# Agent handoff: whiteboard

open-source canvas for thoughtful software design

## Start here

Repository: https://github.com/nihitkaul/whiteboard. Inspected default branch: `main`. Handoff prepared September 27, 2026 from checked-in sources.

This is a fork. Preserve upstream contribution instructions and licenses. This sweep adds documentation only; it does not synchronize upstream branches or release anything.

Read [README.md](README.md) before running the app. Those documents carry project-specific setup details and known limitations.

Existing [AGENTS.md](AGENTS.md) remains authoritative for repository-specific development rules.

## Architecture map

- `apps/`: workspace applications.
- `docs/`: design and operational documentation.
- `packages/`: workspace packages.
- `packaging/`: tracked project subtree; inspect its source and local documentation before edits.
- `scripts/`: developer/operational commands.
- `tools/`: tracked project subtree; inspect its source and local documentation before edits.

## Install, run and validate

### package.json

Working directory: `.`. Runtime constraints: `{"node": ">=24 <25", "pnpm": ">=11 <12"}`.

Install with `pnpm install --frozen-lockfile`. Respect existing AGENTS.md command restrictions before running scripts.

Available scripts from this manifest (reference, not a deployment instruction):

- `pnpm run dev` → `REVIEW_DESKTOP_DEV_FAST=1 pnpm desktop:build && pnpm desktop:run`
- `pnpm run dev:background` → `DEV_FAST_REVIEW_DESKTOP_BACKGROUND=1 pnpm dev`
- `pnpm run clean` → `node scripts/clean-review-desktop.mjs`
- `pnpm run desktop:build` → `pnpm --filter @dev.fast/review-desktop app:build`
- `pnpm run desktop:run` → `pnpm --filter @dev.fast/review-desktop app:run`
- `pnpm run desktop:watch` → `pnpm --filter @dev.fast/review-desktop app:watch`
- `pnpm run desktop:package:linux` → `pnpm --filter @dev.fast/review-desktop app:package:linux`
- `pnpm run review` → `pnpm --filter @dev.fast/review review`
- `pnpm run format` → `oxfmt --write "apps/**/*.{ts,tsx,js,jsx,json,css}" "!apps/review-desktop/code-oss/**" "packages/**/*.{ts,tsx,js,jsx,json,css}" "!packages/review/app/icons/dev-fast.icon/**" "*.json" ".*.json"`
- `pnpm run format:check` → `oxfmt --check "apps/**/*.{ts,tsx,js,jsx,json,css}" "!apps/review-desktop/code-oss/**" "packages/**/*.{ts,tsx,js,jsx,json,css}" "!packages/review/app/icons/dev-fast.icon/**" "*.json" ".*.json"`
- `pnpm run lint` → `oxlint --disable-nested-config .`
- `pnpm run ci` → `pnpm --filter @dev.fast/review-desktop app:build && pnpm --filter @dev.fast/review check:tutorial && pnpm lint && pnpm format:check && pnpm typecheck && pnpm test`
- `pnpm run test` → `node --test "scripts/**/*.test.mjs" && pnpm -r --if-present test`
- `pnpm run typecheck` → `pnpm -r --workspace-concurrency=1 --if-present typecheck`
- `pnpm run build` → `pnpm -r --if-present build`

## Configuration, data and service plumbing


Never commit provider credentials, OAuth secrets, personal records, local browser profiles or dependency directories. Deployment is a separate operation from pushing source: a git push does not prove the app is live.

## Existing design and operations references

- [AGENTS.md](AGENTS.md)
- [CLAUDE.md](CLAUDE.md)
- [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)
- [CONTEXT.md](CONTEXT.md)
- [CONTRIBUTING.md](CONTRIBUTING.md)
- [SECURITY.md](SECURITY.md)
- [docs/privacy.md](docs/privacy.md)
- [docs/telemetry.md](docs/telemetry.md)

## Handoff and next-change checklist

This sweep checked repository structure, documentation and command/configuration declarations. It did not certify a fresh install, live credentials, every deployment or every test suite. Treat existing verification notes as dated evidence, not a current production guarantee.

For the next change: read local AGENTS.md rules; inspect git status and branch; reproduce the relevant behavior; update source and focused tests; run the declared relevant checks; update README/architecture/runbook with changed commands, data flow and limitations; commit only reviewed files; push and verify the remote commit. Record any unresolved setup dependency or test failure explicitly. Preserve repository visibility and unrelated work.
