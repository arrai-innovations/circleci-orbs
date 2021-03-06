# CircleCI Orbs

![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=for-the-badge)

This repository contains circleci orbs that Arrai Innovations publishes to the CircleCI Orb registry. While available for public consumption, these are tailored towards our CI process. These orbs are published into the _arrai_ namespace.

_Note to contributors_: The Orb Registry is public; private data should be passed via variables configured in the CI interface or stored in the appropriate private repo.

<!-- prettier-ignore-start -->
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Available Orbs](#available-orbs)
  - [badass](#badass)
  - [eslint](#eslint)
  - [deepcode](#deepcode)
  - [flake8](#flake8)
  - [prettier](#prettier)
  - [pytest](#pytest)
  - [utils](#utils)
- [Developing Orbs](#developing-orbs)
- [Publishing Orbs](#publishing-orbs)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
<!-- prettier-ignore-end -->

## Available Orbs

### badass

This Orb provides an environment for running our BMS/Django tests. Not likely to be useful for testing Django instances not built or based on BMS. For a description of the Orb, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/badass).

### eslint

Runs eslint on project code. Note that any warnings are treated as job failures. For more details, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/eslint).

### deepcode

Runs the [DeepCode CLI](https://github.com/DeepCodeAI/cli) on project code. Note that suggestions of any severity (info, warning, or critical) are treated as job failures. For more details, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/deepcode).

### flake8

Provides functionality for running flake8 on project code. Errors and warnings are reported in separate steps. Note that warnings are treated as job failures. For a description of the Orb, available steps, parameters, etc, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/flake8).

### prettier

Provides functionality for running prettier on project code. For more details, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/prettier).

### pytest

Provides generic test environment for pytest based tests that have dependencies installed using `pipenv`. For more details, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/pytest).

### utils

This orb provides utility functions such as status badging, file uploads, and ssh key import. This is required by the other orbs. For information on the available utility functions, refer to the [documentation](https://circleci.com/orbs/registry/orb/arrai/utils).

## Developing Orbs

This repository uses git hooks via the node module `husky`. These hooks keep the orb `.yml` formatted using `prettier`. They also enforce our commit message rules via `commitlint`. You can install these hooks by running the following command:

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
