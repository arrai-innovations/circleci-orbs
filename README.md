# CircleCI Orbs

This repository keeps track of the Orbs Arrai Innovations publishes to the CircleCI Orb registry. While available for public consumption, these are tailored towards our CI process. These orbs are published into the *arrai* namespace.

*Note to contributors*: The Orb Registry is public; private data should be passed via variables configured in the CI interface or stored in the appropriate private repo.

## Available Orbs

This repository currently contains the following Orbs:
- [badass](https://circleci.com/orbs/registry/orb/arrai/badass)
- [flake8](https://circleci.com/orbs/registry/orb/arrai/flake8)
- [eslint](https://circleci.com/orbs/registry/orb/arrai/eslint)
- [deepcode](https://circleci.com/orbs/registry/orb/arrai/deepcode)
- [utils](https://circleci.com/orbs/registry/orb/arrai/utils)

### badass
This Orb provides an environment for running our BMS/Django tests. Not likely to be useful for testing Django instances not built or based on BMS. For a description of the Orb, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/badass).

### flake8
Provides functionality for running flake8 on the project code. Errors and warnings are reported in separate steps. Note that warnings are treated as job failures. For a decription of the Orb, available steps, parameters, etc, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/flake8).

### eslint
Runs eslint on the project code. Note that any warnings are treated as job failures. For more details, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/eslint).

### deepcode
Runs the [DeepCode CLI](https://github.com/DeepCodeAI/cli) on the project code. Note that suggestions of any severity (info, warning, or critical) are treated as job failures. For more details, refer to the generated [documentation](https://circleci.com/orbs/registry/orb/arrai/deepcode).

### utils
This orb provides utility functions such as status badging, file uploads, and ssh key import. This is required by the other orbs. For information on the available utility functions, refer to the [documentation](https://circleci.com/orbs/registry/orb/arrai/utils).

## Publishing Orbs

There are a few things to keep in mind when publishing new Orbs to the registry. Orbs are to be published using [semver](https://devhints.io/semver). Versioning is taken care of automatically by specifying one of *patch*, *minor*, or *major* when publishing. Publishing a new release works by promoting a previously published dev version. Since references to Orbs are versioned, a new release has no impact on existing project configurations or Orbs.

In order to publish Orbs to the registry, install the [circleci](https://circleci.com/docs/2.0/creating-orbs/#installing-the-cli-for-the-first-time) CLI application. Run `circleci setup` to configure the tool once installed.

If you are creating a new Orb, you must first create it in the registry: `circleci orb create arrai/example`. Skip this if you're updating an existing Orb.

After making the requisite changes, you can check for syntactic validity by running: `circleci orb validate example.yml`. Note that the registry will prevent you from publishing Orbs containing syntax errors.

You can then publish a dev version of your Orb: `circleci orb publish example.yml arrai/example@dev:1`. You can now reference this Orb in project-specific configs or other Orbs. Unlike release Orbs, development Orbs are mutable and will be deleted after 90 days.

Once you're ready to promote your Orb to release, determine whether this counts as a patch, minor, or major release; this will be passed into the promote command: `circleci orb publish promote arrai/example@dev:1 patch`. The command will return the version number used for the Orb; use this to reference the new Orb in your project CI configurations.
