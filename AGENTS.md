# Repository Guidelines

## Project Structure & Module Organization

This workspace contains packaged applications, datasets, drivers, and deployment helpers rather than a single source tree. Treat top-level `*.zip` and `*.7z` files as immutable artifacts; do not edit archives in place. Operational files live at the root:

- `start.sh` and `stop.sh` manage the `mkuserver` process.
- `server.service` defines its systemd unit.
- `pack.sh` gathers shared-library dependencies for `lsserver`.
- `auto-del-disk.sh` enforces a recording-directory size limit.
- `install.sh` is a vendored NVM installer; avoid project-specific edits to it.

Place new source code in a named project directory with its own `README.md`, not loose at the root. Keep generated data and binaries out of source directories.

## Build, Test, and Development Commands

There is no repository-wide build or test runner. Validate only the component you change:

- `bash -n script.sh` checks Bash syntax.
- `sh -n start.sh pack.sh` checks POSIX shell syntax.
- `shellcheck script.sh` performs static analysis when ShellCheck is installed.
- `systemd-analyze verify server.service` validates the unit file; it may require systemd tooling.

Do not run these scripts casually: they use machine-specific paths, manage processes, copy libraries, or delete files.

## Coding Style & Naming Conventions

Use four-space indentation in shell control blocks, quote variable expansions, and prefer descriptive uppercase names for constants (for example, `DISK_SPACE_THRESHOLD`). New scripts should use lowercase kebab-case names, include an appropriate shebang, and enable safe behavior where compatible (`set -eu`). Extract host-specific paths into documented variables near the top of each script.

## Testing Guidelines

For shell changes, run the relevant syntax check and ShellCheck, then test against a temporary directory or disposable process. Cover success and failure paths, especially missing PID files, unavailable executables, paths containing spaces, and disk-cleanup boundaries. Never test deletion logic against production recordings.

## Commit & Pull Request Guidelines

No prior Git history was available when this repository was initialized, so no existing commit convention could be inferred. Use short, imperative subjects such as `Harden disk cleanup path handling`. Pull requests should identify affected artifacts, list validation commands and results, explain changes to absolute paths or service behavior, and link the relevant issue. Include logs for service changes; screenshots are only needed for user-visible applications.

## Security & Configuration Tips

Do not commit credentials, private keys, machine-specific PID files, or unpacked personal data. Verify archive provenance and checksums before replacing binary or dataset packages.

## Agent skills

### Issue tracker

Issues and PRDs are tracked in GitHub Issues at `LMIXR/CV_Deployment_skill`. See `docs/agents/issue-tracker.md`.

### Triage labels

This repo uses the default triage label vocabulary. See `docs/agents/triage-labels.md`.

### Domain docs

This repo uses a single-context domain documentation layout. See `docs/agents/domain.md`.

## Resource Safety on This Host

This workstation has 16 GiB of RAM. Keep Codex workloads bounded so the desktop remains responsive:

- The user controls the number of independent Codex CLI sessions; do not enforce a single-instance restriction.
- Do not impose a fixed subagent-concurrency limit below the Codex client default; let the shared Codex memory pool bound aggregate resource use. Use only one subagent for image- or video-heavy work.
- Use `fork_turns="none"` or the smallest useful positive turn count. Never use `fork_turns="all"` after images or large tool outputs have entered the thread.
- Inspect at most two images per `view_image` call. Prefer `detail="high"`; use `detail="original"` only when exact pixels are required.
- Never print base64, binary data, whole large logs, or multi-megabyte command output into the conversation. Filter first with `rg`, `sed`, `head`, or `tail`, and keep tool output budgets at or below 10,000 tokens.
- Start a fresh thread instead of resuming a thread whose rollout is unusually large or whose UI/database operations have become slow.
