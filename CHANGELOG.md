# Changelog

## added/modified:

* chore/ci: `VERSION` file starting at v1.0.0, checked on every pull request, with each merge to main tagged with that version.
* fix/readme-badge: the Copier badge in generated READMEs links to karshosphere/template-go.
* feature/run-script: generated projects ship a run.sh for building, formatting, testing and release builds, with release targets chosen at generation.
* feature/github-ci: generated projects ship the shared GitHub CI and a VERSION file, which copier update leaves alone.
* fix/project-builds: generated projects build, test and cross-compile out of the box, with a go.mod, gofmt-clean code, a pure Go SQLite driver and a dev container that installs Go.
* chore/renovate-grouping: Renovate batches minor, patch and digest updates into one weekly pull request and reminds the reviewer to bump VERSION.
* chore/ci-update: shared CI v1.1.1, with generated projects and this template both following the shared Renovate settings.
* feature/makefile: generated projects ship a Makefile with build, format, format-dry-run, test and release targets in place of run.sh, with the release builds in scripts/release.sh, make in the dev container and the shared CI calling make.
* feature/root-answers-file: generated projects keep their Copier answers in `.copier-go-answers.yml` at the root rather than in `.copier-generic-project/`; existing projects move the file once before their next update.
* fix/dockerfile-workdir: copier update no longer conflicts on the Dockerfile; existing projects resolve it once on their next update.
* fix/devcontainer-timezone: the dev container, and CI with it, starts on hosts that have no /etc/timezone.
* fix/bash-history-mount: shell history in the dev container persists between sessions.
* feature/plain-version: VERSION holds a plain X.Y.Z here and in generated projects, with CI adding the v for tags; existing projects remove the v from VERSION once.
