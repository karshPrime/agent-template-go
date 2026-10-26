# Go Template

[![Copier](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-grayscale-inverted-border-orange.json)](https://github.com/copier-org/copier)

A [Copier](https://copier.readthedocs.io/en/stable) template for Go projects.


## Create a Project

```bash
$ uv tool install copier
$ copier copy --trust gh:karshosphere/template-go path/to/project
```

Copier asks for:
* **Project Name** and an optional **Project Description**.
* **Application Type:** CLI (cobra), TUI (bubbletea) or WebServer (gin).
* **Database Support:** SQLite via GORM, or none.
* **Release Targets:** platforms `make release` builds for, or none. `windows-arm32` is not offered, as Go no longer supports it.

`--trust` lets the template run `git` and `go mod tidy`. Without Go installed, run `go mod tidy` in the dev container afterwards and commit `go.mod` and `go.sum`.

Your name, email and GitHub user come from `~/.config/copier/settings.yml`, and are left empty without it:

```yaml
defaults:
  user_name: "karsh"
  user_email: "karshmail@icloud.com"
  github_user: "karnull"
```


## Update a Project

From the project root:

```bash
$ copier update --defaults --answers-file .copier-go-answers.yml
```

Older projects need a one-off step first:
* **Before 2.1.0:** move the answers file to the root with `git mv .copier-generic-project/.copier-go-answers.yml .copier-go-answers.yml`.
* **Before 3.0.0:** drop the `v` from `VERSION` with `sed -i 's/^v//' VERSION`.


## What a Project Gets

* A `Makefile`:
  * `make build` builds the binary into `build/`.
  * `make format` formats the sources; `make format-dry-run` fails if any need it.
  * `make test` runs the tests.
  * `make release` cross-compiles each release target into `dist/` with `scripts/release.sh`.
* A dev container with Go and make.
* The shared CI from [template-github-ci](https://github.com/karshosphere/template-github-ci): it runs the four make targets in the dev container, requires a `VERSION` bump on every pull request, and publishes a GitHub release on each merge to main.
* `VERSION`, starting at `0.1.0`, and a `renovate.json` using the shared Renovate settings. The project owns both; updates never overwrite them.


## Maintaining the Template

* Bump `VERSION`, a plain `X.Y.Z`, on every branch: `Z` for fixes, `Y` for features and chores, `X` for changes that break `copier update` in existing projects. CI checks it and tags each merge to main `vX.Y.Z`.
* Renovate keeps the pinned actions and images current, grouping minor updates into one weekly pull request. It never touches `VERSION`.
* Bring in a newer release of the shared CI from the repository root with `copier update -a .github/.copier-ci-answers.yml template`.
