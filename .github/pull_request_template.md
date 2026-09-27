<!--
Written for any collaborator reading this cold — not for whoever was in the authoring session.
Rules: https://github.com/ramaai-dev/.github/blob/main/.github/CONTRIBUTING.md#writing-issues-and-prs
  · impersonal — no "you" / "I" / "per your note" / session narrative
  · roles, not names — "maintainer", "reviewer"; use the Reviewers and Assignees fields to address a person
  · no site network facts (AE titles, real IPs, ports), no PHI, no personal paths or devices
  · a hospital codename is fine in this body — never in CHANGELOG, release notes, or anything that ships
Title: Conventional Commit — e.g. `fix(pacs): await capped-collection creation`
Delete any section that does not apply. Keep it short — link the design doc or ADR instead of restating it.
-->

**✨ Intent:** <!-- Optional — delete when the title already says it. A sentence or two: what is true after merge that is not true now. -->

## Summary

- **Problem:**
- **Change:**
- **Not in this PR:**

Closes #

## Verification

- **Dry gate** (hermetic — lint, types, unit, mocked integration):
- **Live gate** (a real running service — describe the environment generically):
- **Not verified:**

## Risk & compatibility

Answer each `Yes` or `No`.

- One-way door — hard to roll back (data migration, deletion, published contract or release):
- PHI boundary or de-identification path touched:
- Secrets, authentication, or network egress changed:
- Config keys, data schema, or API contract changed:
- Upgrade path of deployed sites affected (install scripts, data migration, a manual step):
- Hospital codename or name added to anything that ships or publishes (source, config or examples, CHANGELOG, API specs):

If any `Yes` — the blast radius (who or what breaks if this is wrong), its mitigation, and the exact upgrade steps:

## Open questions for review

<!-- Decisions a reviewer must make. One neutral question each, with the options. Delete if none. -->
