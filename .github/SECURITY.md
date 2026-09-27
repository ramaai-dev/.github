# Security

This is the default security policy for every repository in
[ramaai-dev](https://github.com/ramaai-dev). A repository with a `SECURITY.md` of its own follows
that one instead.

## What to report privately

- A vulnerability that could be exploited — authentication bypass, exposed secret, injection,
  unauthenticated service, PHI reachable from outside its boundary.
- A leak in the record — PHI, credentials, or site network facts (AE titles, addresses, ports,
  hostnames) posted in an issue, PR, comment, commit, or log.

## How

**Do not open an issue or PR for it, and do not quietly edit the leak away** — an edit keeps the
previous text in the history, and a public report tells others where to look.

Contact a maintainer of the affected repository, or an owner of the ramaai-dev organization,
directly. Include:

- the repository and the location (file and line, issue or PR number, commit SHA);
- what is exposed or exploitable, and since when, if known;
- whether it has reached anything that ships or publishes (a release, a package, a public page).

## What happens next

A maintainer confirms receipt, contains it first — rotates the credential, deletes the revision or
commit, pulls the release — and only then fixes the cause. The fix lands through a normal PR whose
body describes the class of problem without repeating the leaked data.
