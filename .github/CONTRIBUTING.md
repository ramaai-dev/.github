# Contributing

This is the default guide for every repository in [ramaai-dev](https://github.com/ramaai-dev). A
repository with a `CONTRIBUTING.md` of its own follows that one instead — look there for its dev
setup, branching model, and gates.

- **Commits and PR titles:** [Conventional Commits](https://www.conventionalcommits.org/) — for
  example `fix(parser): handle empty input`.
- **One topic per PR.** For anything beyond a small fix, open an issue first so the approach is
  agreed before the work is done.
- **Search first.** A comment on an open issue beats a duplicate.

## Writing issues and PRs

Issues and PRs are the project's shared, durable record. Each one is read by collaborators who were
not present when it was written — often months later, often by someone deciding whether a change is
safe to install at a hospital. Write for that reader.

This applies equally to people and to AI coding agents. An agent's conversation with its operator is
not part of the record: what a session decided is restated as fact, and nothing in an issue or PR
addresses the operator.

### 1. Impersonal voice

No second person, no first-person singular, no narrative of how the work went.

| Instead of | Write |
| --- | --- |
| "Flagged for your call — not changed" | "**Open question:** the release notes name a site. Generalise before tagging? Options: …" |
| "Both cloud providers, per your note" | "Both cloud providers are pinned, because …" |
| "Three bugs the lab caught, all mine" | "Three defects found in manual VM testing:" |
| "This session's commit (`119971f`)" | "`119971f` — …" |
| "Happy to take either if you want to assign it" | *(delete — that is what the Assignees field is for)* |

### 2. Roles, not names

"Needs a maintainer decision", "manual visual check by a maintainer", "reported by an operator" —
never a name or initials. To address a specific person use GitHub's own mechanics: **Assignees**,
**Reviewers**, or an @mention in a comment. The body stays true after the team changes.

### 3. No personal environment

No home-directory paths (`/Users/…`, `~/…`), no personal machine names, no tooling that is not
committed to the repository. Describe an environment so that anyone can rebuild it:
"Ubuntu 24.04 VM, MongoDB 8.0", "the repository's live gate".

Cost or access constraints belong to whoever holds the budget, not to the record — leave them out.

### 4. Site data — codenames yes, network facts never

RAMAAI software runs inside hospitals. What may be written about a site depends on the class of the
information, not on the repository being private: *the classification, not the container, decides*.

| Class | What it covers | Where it may appear |
| --- | --- | --- |
| **Internal** | a hospital's codename (preferred) or name, its PACS vendor, what its PACS was observed to do | working records — issues, PRs, commit messages, `docs/` — of private repositories |
| **Semi-secret** | PACS address, port, AE titles, test accession, site files, site logs | the team's private site-configuration store only — never any repository |
| **PHI** | patient names, HN/MRN, accession numbers, study UIDs, DICOM that has not been de-identified | nowhere |

**Internal does not mean shippable.** A codename never goes into anything that leaves the team:
source, config, or examples that enter a package; `CHANGELOG.md` and release notes; API specs;
published documentation; any public repository — including this one. Those are read at other
hospitals.

For network facts use stand-ins — `PACS_AET`, and the documentation ranges `192.0.2.0/24` and
`198.51.100.0/24`. A screenshot counts as text: crop the address bar and any AE title.

Editing an issue does not remove a leak: the previous text stays in the edit history until a
maintainer deletes that revision. Report a leak as described in [SECURITY.md](SECURITY.md) instead
of quietly fixing it.

### 5. Evidence over inference

Say what was observed and how — the command, the log line, the code location as
`path/to/file.ext:123`. Where something is not known, write `Unknown` rather than a plausible guess,
and say what was ruled out. Keep *verified* and *not verified* apart; the PR template has a slot for
each.

### 6. Short

A body is a summary with links, not a transcript. Reasoning that should outlive the change belongs in
`docs/design/` or an ADR; link it.

## Filing from the command line

`gh` cannot see issue forms, and `--body` bypasses the PR template, so the structure has to be
reproduced by hand. Done properly, the result is indistinguishable from one filed on the web.

**Issue** — use the form's field labels, in order, as `###` headings; omit optional fields that are
empty; set the type explicitly:

```sh
gh issue create --type Bug --title "…" --body-file body.md
#   --type Bug | Feature | Task        a spike is --type Task --label spike
#   --parent <issue-url>               attach as a sub-issue of a parent issue
#   --label security                   facets only — the type replaces the bug/enhancement labels
```

`--label` fails on a label the repository lacks; create it first or leave it off.

| Form | Headings |
| --- | --- |
| Bug | Summary · Reproduce · Actual · Expected · Environment · Logs · Analysis · Impact |
| Feature | Problem · Proposal · Alternatives considered · Done when · Out of scope · Compatibility · References |
| Task | Goal · Context · Work · Done when · Out of scope |
| Spike | Question · Unblocks · Timebox · Approach · Out of scope |

A repository with its own `.github/ISSUE_TEMPLATE/` uses its own forms, not these — read its YAML.

**Pull request** — fill the PR template that applies to the target repository and pass it with
`--body-file`. Delete sections that do not apply; do not add a different set of headings.
