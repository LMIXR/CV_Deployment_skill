# Issue tracker: GitHub

Issues and PRDs for this repo live as GitHub issues. Use the `gh` CLI for all operations.

## Conventions

- **Create an issue**: `gh issue create --title "..." --body "..."`. For multi-line bodies, write the exact text to a temporary file and use `--body-file <path>`.
- **Read an issue**: `gh issue view <number> --json number,title,body,labels,comments --jq '{number, title, body, labels: [.labels[].name], comments: [.comments[].body]}'`.
- **List issues**: `gh issue list --state open --limit 100 --json number,title,body,labels,comments --jq '[.[] | {number, title, body, labels: [.labels[].name], comments: [.comments[].body]}]'` with appropriate `--label` and `--state` filters. The limit of 100 is an initial cap, not a completeness guarantee. If the returned array contains as many issues as the requested limit, rerun with the same filters and a larger `--limit`; repeat until a successful response contains fewer issues than the limit. Count before any local filtering and use the final complete result. A failed or capped listing is incomplete and must not be used to conclude that no eligible issues remain.
- **Comment on an issue**: `gh issue comment <number> --body "..."`
- **Apply / remove labels**: `gh issue edit <number> --add-label "..."` / `--remove-label "..."`
- **Close**: `gh issue close <number> --comment "..."`

Target repository: `LMIXR/CV_Deployment_skill` (https://github.com/LMIXR/CV_Deployment_skill).

Use `--repo LMIXR/CV_Deployment_skill` with `gh issue` and `gh pr` commands. Use `repos/LMIXR/CV_Deployment_skill/...` for `gh api` endpoints. This also works before a local Git remote is configured.

## Pull requests as a triage surface

**PRs as a request surface: no.** _(Set to `yes` if this repo treats external PRs as feature requests; `$triage` reads this flag.)_

When set to `yes`, PRs run through the same labels and states as issues, using the `gh pr` equivalents:

- **Read a PR**: `gh pr view <number> --comments` and `gh pr diff <number>` for the diff.
- **List external PRs for triage**: `gh api --paginate 'repos/LMIXR/CV_Deployment_skill/pulls?state=open&per_page=100' --jq '.[] | select(.author_association == "CONTRIBUTOR" or .author_association == "FIRST_TIME_CONTRIBUTOR" or .author_association == "NONE")'`. The REST API exposes `author_association`; this keeps the existing external-author categories and drops `OWNER`/`MEMBER`/`COLLABORATOR`. For each retained PR, fetch the triage fields and comment bodies with `gh pr view <number> --repo LMIXR/CV_Deployment_skill --json number,title,body,labels,author,comments`; the REST list response does not contain comment bodies.
- **Comment / label / close**: `gh pr comment`, `gh pr edit --add-label`/`--remove-label`, `gh pr close`.

GitHub shares one number space across issues and PRs, so a bare `#42` may be either — resolve with `gh pr view 42` and fall back to `gh issue view 42`.

## When a skill says "publish to the issue tracker"

Create a GitHub issue.

## When a skill says "fetch the relevant ticket"

Follow the **Read an issue** procedure above.

## Wayfinding operations

Used by `$wayfinder`. The **map** is a single issue with **child** issues as tickets.

- **Map**: a single issue labelled `wayfinder:map`, holding the Notes / Decisions-so-far / Fog body. `gh issue create --label wayfinder:map`.
- **Child ticket**: an issue linked to the map as a GitHub sub-issue (`gh api` on the sub-issues endpoint). Where sub-issues aren't enabled, add the child to a task list in the map body and put `Part of #<map>` at the top of the child body. Labels: `wayfinder:<type>` (`research`/`prototype`/`grilling`/`task`). Once claimed, the ticket is assigned to the driving dev.
- **Blocking**: GitHub's **native issue dependencies** — the canonical, UI-visible representation. Add an edge with `gh api --method POST repos/<owner>/<repo>/issues/<child>/dependencies/blocked_by -F issue_id=<blocker-db-id>`, where `<blocker-db-id>` is the blocker's numeric **database id** (`gh api repos/<owner>/<repo>/issues/<n> --jq .id`, _not_ the `#number` or `node_id`). GitHub reports `issue_dependencies_summary.blocked_by` (open blockers only — the live gate). Where dependencies aren't available, fall back to a `Blocked by: #<n>, #<n>` line at the top of the child body. A ticket is unblocked when every blocker is closed.
- **Frontier query**: completely enumerate open issues using the **List issues** procedure above before filtering candidates. Then restrict the result to the map's children using its complete sub-issue list (fetch every page) or task list. The listing does not retain eligibility fields: for each candidate, fetch `gh api repos/LMIXR/CV_Deployment_skill/issues/<n>` and retain `assignees`, `issue_dependencies_summary.blocked_by`, `state`, and `body` before selection. Require a successful response with an explicit `assignees` array; only an empty array establishes that the ticket is unclaimed. Require an explicit nonnegative integer `issue_dependencies_summary.blocked_by`; zero establishes no open native blockers, and a positive value excludes the ticket. Only where native dependencies are known to be unavailable and the body convention is in use, inspect the fetched body's `Blocked by` line and fetch each referenced blocker with `gh api repos/LMIXR/CV_Deployment_skill/issues/<blocker-number>` (use the referenced repository for cross-repository blockers), retaining its `state`; every listed blocker must be confirmed closed. Under that fallback convention, no listed blockers means unblocked. A failed fetch, missing or null eligibility field, or unreadable blocker state means unknown, not unclaimed or unblocked; a missing native summary alone does not establish that the fallback applies. Exclude confirmed closed, assigned, or blocked tickets; among confirmed open, unclaimed, unblocked children, first in map order wins. If an earlier child's eligibility is unknown, report the uncertainty before selecting a later child. Do not conclude that the frontier is empty from an incomplete enumeration or unresolved eligibility status.
- **Claim**: `gh issue edit <n> --add-assignee @me` — the session's first write.
- **Resolve**: `gh issue comment <n> --body "<answer>"`, then `gh issue close <n>`, then append a context pointer (gist + link) to the map's Decisions-so-far.
