# Changelog

All notable changes to this project will be documented in this file.

## [0.9.0] - 2026-09-10

<!-- USER-EDITABLE SECTION START -->
### Highlights

- **Synced to upstream `agegr/pi-web` v0.9.0** (63 commits since v0.8.11). The fork now ships the workspace **web terminal** (xterm.js + node-pty, with restore/reconnect/restart and process cleanup), **full-text session search**, **quoted selections** (ask about selected assistant text in place, or branch a quoted chat from that point), **plugin update checks** with single and bulk updates, and **chat appearance controls** (width, font size, default thinking expansion).
- **First release under the fork's own npm scope.** Published as `@cad0p/pi-web-agegr` — upstream owns `@agegr/pi-web`, so the fork publishes under `@cad0p`. CI, release, and validation run through `cad0p/semver-calver-release` with OIDC trusted publishing; calver prereleases land on the `next` dist-tag, curated base releases on `latest`.
- **pnpm replaces npm** for development, CI, and the release pipeline (`package-lock.json` → `pnpm-lock.yaml`).

### Added

- Workspace terminal tabs in the file panel — restoration, reconnection, restart, and reliable process cleanup ([#695](https://github.com/agegr/pi-web/pull/695))
- Full-text session search with match snippets, direct message jumps, and cross-window refresh
- Ask about a selected assistant reply in the current chat, or create a quoted branch chat from that point ([#698](https://github.com/agegr/pi-web/pull/698))
- Plugin version checks with individual and bulk updates ([#611](https://github.com/agegr/pi-web/pull/611))
- `Alt`/`Option`+`Enter` sends a follow-up while streaming; unsupported image attachments now show a warning
- `PI_WEB_IDLE_TIMEOUT_MS` to tune or disable idle session reaping ([#665](https://github.com/agegr/pi-web/pull/665))
- Inline video previews; completed Mermaid diagrams render as previews with SVG download ([#655](https://github.com/agegr/pi-web/pull/655), [#693](https://github.com/agegr/pi-web/pull/693))
- Built-in subagent Settings → Agents surface and runtime toggle re-enabled (still off by default)

### Fixed

- Preserved complete history, the latest response, and minimap navigation across compaction and pagination
- Preserved unsent text/image drafts for new sessions and restored independent reading positions per session
- Idle cleanup no longer reaps sessions with extension-owned background work; deleting a session works when its parent file is missing
- Sub-path deployments, Windows drive-root access, and Ctrl/Cmd-click on encoded local file links
- Mobile scrolling no longer shifts the page around the keyboard while streaming

### Changed

- pi dependencies `0.84.3` → `0.85.1`; new runtime dependencies `@xterm/xterm`, `@xterm/addon-fit`, `node-pty`, `semver`
- The published package now runs a `postinstall` step (`node-pty` ships macOS `spawn-helper` binaries without executable bits)
- eslint disables `react-hooks/preserve-manual-memoization` — pnpm resolves `eslint-plugin-react-hooks@7.1.1`, whose recommended config promotes the React Compiler rule to an error

### Fork

- CI: pnpm + Node 24 `test` job (typecheck, lint, unit tests) **and** the upstream Playwright e2e suite; both green on the sync PR
- `pnpm-workspace.yaml` allow-lists the `node-pty` and `esbuild` install scripts for pnpm 11
- Verified before merge: `pnpm install --frozen-lockfile`, `tsc --noEmit`, `eslint`, `pnpm test` — 979 passing (was 844)
<!-- USER-EDITABLE SECTION END -->

### ⚙️ Miscellaneous Tasks

- Migrate to pnpm and add semver-calver-release npm publishing (closes #2)
- *(sync)* Merge upstream/main v0.9.0 into the fork (closes #4)


