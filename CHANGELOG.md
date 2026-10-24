# Changelog

## added/modified:

* chore/ci: `VERSION` file starting at v1.0.0, checked on every pull request, with each merge to main tagged with that version.
* fix/readme-badge: the Copier badge in generated READMEs links to karshosphere/template-go.
* feature/run-script: generated projects ship a run.sh for building, formatting, testing and release builds, with release targets chosen at generation.
* feature/github-ci: generated projects ship the shared GitHub CI and a VERSION file, which copier update leaves alone.
* fix/project-builds: generated projects build, test and cross-compile out of the box, with a go.mod, gofmt-clean code, a pure Go SQLite driver and a dev container that installs Go.
* chore/renovate-grouping: Renovate batches minor, patch and digest updates into one weekly pull request and reminds the reviewer to bump VERSION.
* chore/ci-update: shared CI v1.1.1, with generated projects and this template both following the shared Renovate settings.
