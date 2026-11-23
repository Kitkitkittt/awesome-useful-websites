# Swarm-ready handoff

Repository: `Kitkitkittt/awesome-useful-websites`. Contract: `swarm-ready/v1`. Source inspection: 2026-11-23.
Default branch: `main`. Inspected base: [f873c5717ca1](https://github.com/Kitkitkittt/awesome-useful-websites/commit/f873c5717ca1adea7dc03051120a2297bb76a08e).

**Status: documented; runtime qualification is unverified.** This file defines an agent workflow. It does not install a shell command, enroll the repository in a scheduler, certify test success, or activate VMs. Follow the current user task and existing repository instructions; retain prior authorization within its actual scope.

## Invoke

Give the working agent this prompt:

```text
swarm ready: <one measurable repository objective>
Read SWARM_READY.md and the applicable AGENTS.md. Continue the current owned
work or ready issue, establish the baseline and acceptance check, then prepare
a bounded worker handoff. Use existing authorized tools and capacity. Report
what is documented, implemented, tested, and observed separately.
```

If a `swarm-ready` skill is installed, load it. Otherwise execute the documented workflow directly. Treat the phrase as an agent instruction unless the installed CLI explicitly advertises it. Inspect help/version before using optional command adapters.

## Repository starting point

Read: [README.md](README.md).

Continue an existing approved issue or a clearly scoped user objective after inspecting the source map below. If none is selected, return the smallest useful improvement and its verifier as the handoff; do not begin a portfolio-wide rewrite.

Start with one writer. Add workers only for disjoint changes or independent experiments whose results can be checked separately. Keep shared interfaces and final integration with one owner.

The base above is an inspection snapshot, not a permanent working branch. Refresh the actual target branch, current issues, incumbent worker and applicable nested instructions before editing. Preserve unrelated changes and upstream/fork boundaries.

## Execution logic

1. **Recover context.** Read the current issue, work order and last evidence-backed handoff. Keep useful work and the active worker. Record source commit, unresolved criteria and the next action; avoid repeating completed investigation.
2. **Define success.** State one outcome, baseline, target, changed paths, verification command and expected result. Keep acceptance criteria and reference data fixed unless the user changes the requirement.
3. **Bound the attempt.** Reuse the existing owner/task/attempt identities, action scope, resource limits, time/cost budget and retry allowance. Do not demand a new user-written permission receipt for already authorized work. If a real capability or grant is missing, name the exact blocked action and continue independent work.
4. **Partition only useful work.** Use one writer per branch/worktree and non-overlapping change scope. Reuse the existing task ledger and dependency graph. Reserve verification capacity before adding workers; avoid recursive worker growth and duplicate coordinators.
5. **Implement and measure.** Make the smallest coherent change. Use differential checks when a trusted reference exists, and deterministic failure simulation when it materially improves reproduction. Record the seed/configuration and counterexamples. Do not weaken tests, rewrite baselines or hide pre-existing failures to claim success.
6. **Verify and integrate.** Verify the exact returned commit independently in a clean environment. Recheck the final integrated revision when changes interact. Follow existing review, merge and deployment rules; a green worker report alone cannot override them. Use the narrowest checks that resolve a concrete risk.
7. **Checkpoint and finish.** Save candidate SHA, evidence, measured outcome, remaining blockers and a precise next action before context/lease expiry. Reconcile lost or duplicate completions before retrying. Release only the run's owned resources after preserving evidence. Stop when the requested outcome is met or a concrete blocker prevents the next required action.

## Verification starting point

From the repository root, run this catalog check with Git and Python 3. It reads the entries between `Tools` and `Contributing` in `README.md`, checks the leading HTTP(S) link in each entry, and rejects new or increased exact-URL duplicates. It preserves historical duplicates and accepts the existing non-bulleted link under `C++`. Use `CATALOG_BASE=HEAD` for uncommitted changes; when reviewing a committed candidate, set it to the locally available pre-change commit instead.

```sh
GIT_NO_LAZY_FETCH=1 CATALOG_BASE=HEAD python3 -IBS - <<'PY'
import os
import re
import subprocess
from collections import defaultdict
from pathlib import Path
from urllib.parse import urlsplit


def catalog(text):
    lines = text.splitlines()
    try:
        start = lines.index("## Tools") + 1
        end = lines.index("# Contributing", start)
    except ValueError:
        raise SystemExit("README.md: missing Tools or Contributing catalog boundary")
    destinations = defaultdict(list)
    for number, row in enumerate(lines[start:end], start + 1):
        if not row.strip() or re.fullmatch(r"#{2,6} .+|<br>", row):
            continue
        match = re.match(r"(?:- )?\[([^\]]+)\]\(([^()\s]+)\)", row)
        if not match or not match[1].strip():
            raise SystemExit(f"README.md:{number}: expected a named catalog link")
        try:
            url = urlsplit(match[2])
            valid = url.scheme in {"http", "https"} and url.hostname
        except ValueError:
            valid = False
        if not valid:
            raise SystemExit(f"README.md:{number}: expected an HTTP(S) URL with a host")
        destinations[match[2]].append(number)
    if not destinations:
        raise SystemExit("README.md: catalog is empty")
    return destinations


base = subprocess.check_output(
    ["git", "cat-file", "blob", f"{os.environ['CATALOG_BASE']}:README.md"],
    encoding="utf-8", timeout=5,
)
before = catalog(base)
after = catalog(Path("README.md").read_text(encoding="utf-8"))
increases = [rows for url, rows in after.items() if len(rows) > max(1, len(before.get(url, ())))]
if increases:
    raise SystemExit(f"README.md: new or increased exact-URL duplicates at line groups {increases}")
print(f"Checked {sum(map(len, after.values()))} catalog entries; no new exact-URL duplicates.")
PY
```

Expect exit 0 and an entry count on success. This is an offline text check, not a link-availability or safety verdict: do not visit linked sites, fetch badges, or run linked code. Review any changed descriptions and table-of-contents anchors separately.

## Required handoff result

Return a concise record with `repository`, `objective`, `issue_or_work_order`, `base_sha`, `candidate_sha`, `owner`, `task_id`, `attempt_id`, `worker/session`, `branch/worktree`, `changed_paths`, `environment`, `resource/budget limits`, `acceptance`, `commands_and_results`, `evidence_refs`, `known_failures`, `blocker_owner`, `next_action`, and `cleanup_status`. Use null/unknown when a field is unavailable; never manufacture evidence or authority.

Keep documentation readiness, command availability, source tests, live environment qualification and accepted outcome as separate states. Count verified outcomes, regressions, elapsed time, cost and human interventions. Commits, lines, tokens and worker count describe activity only.
