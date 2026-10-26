# Changelog

## Added

* 3.0.2
   * a shorter README with the right copy command, gh:karshosphere/template-go
   * the first commit of a new project links to this template
* 3.0.1
   * generated code passes make format-dry-run when no author is set in the Copier settings
* 3.0.0
   * VERSION holds a plain X.Y.Z here and in generated projects, with CI adding the v for tags
   * existing projects remove the v from VERSION once
* 2.1.3
   * shell history in the dev container persists between sessions
* 2.1.2
   * the dev container, and CI with it, starts on hosts that have no /etc/timezone
* 2.1.1
   * copier update no longer conflicts on the Dockerfile
   * existing projects resolve it once on their next update
* 2.1.0
   * generated projects keep their Copier answers in `.copier-go-answers.yml` at the root rather than in `.copier-generic-project/`
   * existing projects move the file once before their next update
* 2.0.0
   * generated projects ship a Makefile with build, format, format-dry-run, test and release targets in place of run.sh
   * release builds live in scripts/release.sh
   * make in the dev container, and the shared CI calls make
* 1.4.0
   * shared CI v1.1.1
   * generated projects and this template both follow the shared Renovate settings
* 1.3.0
   * Renovate batches minor, patch and digest updates into one weekly pull request and reminds the reviewer to bump VERSION
* 1.2.1
   * generated projects build, test and cross-compile out of the box
   * a go.mod, gofmt-clean code and a pure Go SQLite driver
   * a dev container that installs Go
* 1.2.0
   * generated projects ship the shared GitHub CI and a VERSION file, which copier update leaves alone
* 1.1.0
   * generated projects ship a run.sh for building, formatting, testing and release builds
   * release targets chosen at generation
* 1.0.1
   * the Copier badge in generated READMEs links to karshosphere/template-go
* 1.0.0
   * `VERSION` file starting at v1.0.0, checked on every pull request
   * each merge to main tagged with that version
