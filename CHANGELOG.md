# Changelog

## added/modified:

* chore/ci: `VERSION` file starting at v1.0.0, checked on every pull request, with each merge to main tagged with that version.
* fix/readme-badge: the Copier badge in generated READMEs links to karshosphere/template-go.
* feature/run-script: generated projects ship a run.sh for building, formatting, testing and release builds, with release targets chosen at generation.
* feature/github-ci: generated projects ship the shared GitHub CI and a VERSION file, which copier update leaves alone.
