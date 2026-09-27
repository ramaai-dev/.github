# .github

Default [community health files](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)
for every repository in [ramaai-dev](https://github.com/ramaai-dev). GitHub applies a file from here
to any repository that has none of its own of that type.

## What is here

| File | Applies as |
| --- | --- |
| `.github/ISSUE_TEMPLATE/1-bug.yml` | "Bug" form — issue type `Bug` |
| `.github/ISSUE_TEMPLATE/2-feature.yml` | "Feature" form — issue type `Feature` |
| `.github/ISSUE_TEMPLATE/3-task.yml` | "Task" form — issue type `Task` |
| `.github/ISSUE_TEMPLATE/4-spike.yml` | "Spike" form — issue type `Task`, label `spike` |
| `.github/pull_request_template.md` | Default PR description |
| `.github/CONTRIBUTING.md` | Default contributing guide — the writing rules for issues and PRs |
| `.github/SECURITY.md` | Default security policy — private reporting of vulnerabilities and leaks |

## How the defaults behave

- **This repository is public — GitHub requires it.** Everything here, including commit history, is
  readable by anyone. Content must be fit to publish: rules may *mention* hospital codenames, but no
  codename, site, or network fact may appear.
- **`main` is production.** A push takes effect at once in every repository that falls back to
  these files, private ones included. Change through a PR; CI schema-checks the forms.
- **Override is total per type.** A repository with anything in its own `.github/ISSUE_TEMPLATE/`
  gets *none* of the default issue forms. The PR template, `CONTRIBUTING.md`, and `SECURITY.md` are
  each replaced by a repository's own file of the same kind.
- **Defaults are invisible.** They never appear in a repository's file tree or in a clone — only
  in the GitHub web UI, and through the API of *this* repository.
- **Issue types, not type labels.** The forms set the organization's issue types (`Bug`, `Feature`,
  `Task`) instead of the `bug` / `enhancement` labels.
- **Labels must already exist.** The Spike form applies `spike`; on the web, a label missing from a
  repository is skipped silently.
- **Blank issues stay enabled** — GitHub's default, so there is no `config.yml`.
- **CLI and API clients bypass templates.** `gh issue create` cannot use an issue form, and
  `gh pr create --body` applies no PR template. A tool that wants this structure has to ask
  for it, and the two kinds resolve differently:

  - **PR template** — ask GitHub about the *target* repository, not this one. GraphQL
    `repository.pullRequestTemplates { filename body }` returns whichever template applies —
    the target's own, else this default — with the body included.
  - **Issue forms** — the API does not expose forms, so read the YAML from this repository,
    unless the target has anything in its own `.github/ISSUE_TEMPLATE/`, which replaces these
    defaults entirely:

    ```sh
    gh api 'repos/ramaai-dev/.github/git/trees/HEAD?recursive=1' --jq '.tree[].path'
    gh api 'repos/ramaai-dev/.github/contents/.github/ISSUE_TEMPLATE/1-bug.yml' \
      -H 'Accept: application/vnd.github.raw+json'
    ```

    Each field `label` becomes a `###` heading — the same Markdown GitHub renders from a
    submitted form. [CONTRIBUTING → Filing from the command line](.github/CONTRIBUTING.md#filing-from-the-command-line)
    lists them per form.

## Editing

```sh
make validate   # schema-check every issue form and workflow; needs uv
```

An invalid form never reaches the issue chooser, so validate before merging. Keep descriptions and
placeholders generic: these files serve every repository in the organization — code, docs, QMS, and
websites alike.
