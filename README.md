
# Generic Template

[![Copier](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-grayscale-inverted-border-orange.json)](https://github.com/copier-org/copier)

This repository provides a template for creating Go project skeletons. It got a consistent and reproducible starting point which makes it easier to apply improvements when the template is updated.


### Prerequisites

Install the Copier command:
* **Quick option:** `uv tool install copier`
* **Documentation:** https://copier.readthedocs.io/en/stable


### Create New Project

Run the following command:

```bash
$ copier copy --trust --vcs-ref=go git@github.com:karnull/templates path/to/project
```
* **Project Description:** Answer the Copier prompt with an optional plain‑text description of your project.
* **Library Pack:** Optional selection of libraries to include in the project.
* **Release Targets:** Platforms `./run.sh --release` builds for, or none. `windows-arm32` is not offered, as Go no longer supports it.
* The `--trust` option is required because the template runs `git` and `go mod tidy`. Without Go installed, run `go mod tidy` in the dev container afterwards and commit `go.mod` and `go.sum`.


### Default Config

User-specific values are loaded from the global configuration file - `~/.config/copier/settings.yml`. If the file is not present or not saved, empty strings are used as defaults.
```
defaults:
  user_name  : "karsh"
  user_email : "karshmail@icloud.com"
  github_user: "karnull"

```



### Updating a Project

Generated projects keep their Copier answers in `.copier-go-answers.yml` at the project root. From there:

```bash
$ copier update --defaults --answers-file .copier-go-answers.yml
```

Projects generated before the answers file moved keep it in `.copier-generic-project/`. Move it once before updating:

```bash
$ git mv .copier-generic-project/.copier-go-answers.yml .copier-go-answers.yml
```


### Versioning and CI

The template's release version lives in `VERSION` as `vX.Y.Z`. Bump it in every change that should be released:
* `Z` for minor fixes.
* `Y` for minor features and chores.
* `X` for breaking changes, such as renamed questions or moved files that affect `copier update` in existing projects.

GitHub Actions (`.github/workflows/ci.yml`) runs two jobs:
* **version:** on every pull request and push to `main`, checks that `VERSION` holds a single `vX.Y.Z` line.
* **tag:** on push to `main`, tags the merged commit with the version in `VERSION`, so existing projects can move to it with `copier update`. If the tag already exists, nothing is tagged.

The workflow is read-only apart from the tag job, which needs write access to create the tag. It runs on `pull_request`, never `pull_request_target`, so code from a fork never runs with this repository's credentials. Actions are pinned to commit SHAs, and Renovate (`renovate.json`, extending the shared settings in template-github-ci) proposes updates to them weekly. Minor, patch and digest updates come as one grouped pull request and majors on their own; Renovate never touches `VERSION`, so bump it on the pull request before merging.


### Project Tasks

Every generated project has a `run.sh` at its root:
* `./run.sh --build` builds the binary into `build/`.
* `./run.sh --format` formats the Go sources; `--format-dry-run` lists unformatted files and fails if there are any.
* `./run.sh --test` runs the tests.
* `./run.sh --release` cross-compiles one binary per release target into `dist/`.


### GitHub CI

Generated projects ship with the shared workflow from [template-github-ci](https://github.com/karshosphere/template-github-ci), vendored into `template/.github/`. It expects the project's `run.sh` and `.devcontainer/`, requires a `VERSION` bump on every pull request, and publishes a GitHub release on each merge to main. They also ship a `renovate.json` that extends the same shared Renovate settings; the project owns it once created, so it can add its own rules.

To bring in a newer release of the workflow, from this repository's root:

```bash
$ copier update -a .github/.copier-ci-answers.yml template
```
