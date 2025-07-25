# CircleCI Orbs

This repository contains circleci orbs that Arrai Innovations publishes to the CircleCI Orb registry. While available for public consumption, these are tailored towards our CI process. These orbs are published into the _arrai_ namespace.

_Note to contributors_: The Orb Registry is public; private data should be passed via variables configured in the CI interface or stored in the appropriate private repo.

<!-- prettier-ignore-start -->
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Available Orbs](#available-orbs)
  - [badass](#badass)
  - [eslint](#eslint)
  - [flake8](#flake8)
  - [github](#github)
  - [lintinator](#lintinator)
  - [npm](#npm)
  - [pip-audit](#pip-audit)
  - [prettier](#prettier)
  - [pypi](#pypi)
  - [pytest](#pytest)
  - [ruff](#ruff)
  - [safety](#safety)
  - [sentry](#sentry)
  - [utils](#utils)
  - [vueda](#vueda)
- [Developing Orbs](#developing-orbs)
- [Publishing Orbs](#publishing-orbs)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
<!-- prettier-ignore-end -->

## Available Orbs

### badass

[![badass: version][]](https://circleci.com/orbs/registry/orb/arrai/badass)

This Orb provides an environment for running our BMS/Django tests. Not likely to be useful for testing Django instances not built or based on BMS. For a description of the Orb, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/badass).

### eslint

[![eslint: version][]](https://circleci.com/orbs/registry/orb/arrai/eslint)

Runs eslint on project code. Note that any warnings are treated as job failures. For more details, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/eslint).

### flake8

[![flake8: version][]](https://circleci.com/orbs/registry/orb/arrai/flake8)

Provides functionality for running flake8 on project code. Everything is treated as an error. For a description of the Orb, available steps, parameters, etc, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/flake8).

### github

[![github: version][]](https://circleci.com/orbs/registry/orb/arrai/github)

Creates a release on GitHub. For information on configuration parameters, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/github).

### lintinator

[![lintinator: version][]](https://circleci.com/orbs/registry/orb/arrai/lintinator)

Provides commands and jobs for running linters on projects. For information on configuration parameters and available jobs and commands, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/github).

### npm

[![npm: version][]](https://circleci.com/orbs/registry/orb/arrai/npm)

Provides npm utility functions. For information on available functions and configuration parameters, refer to the [documentation](https://circleci.com/orbs/registry/orb/arrai/npm).

### pip-audit

[![pip-audit: version][]](https://circleci.com/orbs/registry/orb/arrai/pip-audit)

Runs `pip-audit` on the project code. Supports `pip`, `pipenv`, and `uv` environments. For details, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/pip-audit).

### prettier

[![prettier: version][]](https://circleci.com/orbs/registry/orb/arrai/prettier)

Provides functionality for running prettier on project code. For more details, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/prettier).

### pypi

[![pypi: version][]](https://circleci.com/orbs/registry/orb/arrai/pypi)

Publishes python packages to a PyPI (or compatible) server. It does not include the build step. It is assumed that some other job builds the packages and stashes the dist folder in a cache. Refer to the [example configuration](/examples/pypi.yml) on how this might look.

For information on configuration parameters, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/pypi).

### pytest

[![pytest: version][]](https://circleci.com/orbs/registry/orb/arrai/pytest)

Provides generic test environment for pytest based tests that have dependencies installed using `pipenv`. For more details, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/pytest).

### ruff

[![ruff: version][]](https://circleci.com/orbs/registry/orb/arrai/ruff)

Installs ruff and runs the validator against the code base. For a description of the Orb, available steps, parameters, etc, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/ruff)

### safety

[![safety: version][]](https://circleci.com/orbs/registry/orb/arrai/safety)

This is now somewhat miss-named; it provides jobs to run `pipenv check` against the installed project. For more details, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/safety).

### sentry

[![sentry: version][]](https://circleci.com/orbs/registry/orb/arrai/sentry)

Publish releases to [Sentry](https://sentry.io/). Note that the `create_release` job uses the following defaults when creating releases:

-   The project slug is assumed to be the same as the repository name.
-   The release version is taken from the tag name.
-   It is assumed that repositories have been configured within the Sentry organisation so that commits can be associated with the release. Refer to the [Sentry documentation on this matter](https://docs.sentry.io/product/cli/releases/#sentry-cli-commit-integration).

For information on how to override these defaults, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/sentry). An [example configuration](/examples/sentry.yml) is provided in the [examples folder](/examples/).

### utils

[![utils: version][]](https://circleci.com/orbs/registry/orb/arrai/utils)

This orb provides utility functions such as status badging, file uploads, and ssh key import. This is required by the other orbs. For information on the available utility functions, refer to the [documentation](https://circleci.com/orbs/registry/orb/arrai/utils).

### vueda

[![vueda: version][]](https://circleci.com/orbs/registry/orb/arrai/vueda)

This orb facilitates the deployment of [`vueda-server`] and [`vueda-client`] applications using our [`vueda-deployer`]. It supports deployments to environments like Dev, Demo, Staging and Production, based on git tags or commits. For more details on how to use this orb, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/vueda).

## Developing Orbs

This repository uses git hooks via the node module `husky`. These hooks keep the orb `.yml` formatted using `prettier`. They also enforce our commit message rules via `commitlint`. Orbs are validated using the [circleci cli tool](https://circleci.com/docs/local-cli/), which must be installed beforehand. You can install these hooks by running the following command:

```console
$ npm install
```

## Publishing Orbs

There are a few things to keep in mind when publishing new Orbs to the registry. Orbs are to be published using [semver](https://devhints.io/semver). Versioning is taken care of automatically by specifying one of _patch_, _minor_, or _major_ when publishing. Publishing a new release works by promoting a previously published dev version. Since references to Orbs are versioned, a new release has no impact on existing project configurations or Orbs.

In order to publish Orbs to the registry, install the [circleci](https://circleci.com/docs/2.0/creating-orbs/#installing-the-cli-for-the-first-time) CLI application. Run `circleci setup` to configure the tool once installed.

If you are creating a new Orb, you must first create it in the registry: `circleci orb create arrai/example`. Skip this if you're updating an existing Orb.

After making the requisite changes, you can check for syntactic validity by running: `circleci orb validate example.yml`. Note that the registry will prevent you from publishing Orbs containing syntax errors.

You can then publish a dev version of your Orb: `circleci orb publish example.yml arrai/example@dev:1`. You can now reference this Orb in project-specific configs or other Orbs. Unlike release Orbs, development Orbs are mutable and will be deleted after 90 days.

Once you're ready to promote your Orb to release, determine whether this counts as a patch, minor, or major release; this will be passed into the promote command: `circleci orb publish promote arrai/example@dev:1 patch`. The command will return the version number used for the Orb; use this to reference the new Orb in your project CI configurations.

[badass: version]: https://badges.circleci.com/orbs/arrai/badass.svg
[eslint: version]: https://badges.circleci.com/orbs/arrai/eslint.svg
[flake8: version]: https://badges.circleci.com/orbs/arrai/flake8.svg
[github: version]: https://badges.circleci.com/orbs/arrai/github.svg
[lintinator: version]: https://badges.circleci.com/orbs/arrai/lintinator.svg
[npm: version]: https://badges.circleci.com/orbs/arrai/npm.svg
[pip-audit: version]: https://badges.circleci.com/orbs/arrai/pip-audit.svg
[prettier: version]: https://badges.circleci.com/orbs/arrai/prettier.svg
[pypi: version]: https://badges.circleci.com/orbs/arrai/pypi.svg
[pytest: version]: https://badges.circleci.com/orbs/arrai/pytest.svg
[ruff: version]: https://badges.circleci.com/orbs/arrai/ruff.svg
[safety: version]: https://badges.circleci.com/orbs/arrai/safety.svg
[sentry: version]: https://badges.circleci.com/orbs/arrai/sentry.svg
[utils: version]: https://badges.circleci.com/orbs/arrai/utils.svg
[vueda: version]: https://badges.circleci.com/orbs/arrai/vueda.svg
[`vueda-server`]: https://github.com/arrai-innovations/vueda-server
[`vueda-client`]: https://github.com/arrai-innovations/vueda-client
[`vueda-deployer`]: https://github.com/arrai-innovations/vueda-deployer
