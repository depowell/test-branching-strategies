# test-branching-strategies

## branching strategy
- `feat/f-###` feature branches branched from `development` to PR back to `development` once complete
- `bugfux/b-###` bugfix branches branched from `development` to PR back to `development` once complete
- `development` used as development branch PRs from feature `feat/` or bugfix `bugfix/` branches target `development`
- `master` branch holds up to date versions of code from production
- release branches PRs from `development` to release branches `release/VERSION_TAG` target deployment to these branches:
  - `env_test`
  - `env_uat`
  - `env_prod`

## semver tagging strategy
refer to [semver](https://semver.org/)
- update __MAJOR__ version when you make incompatible API changes
- update __MINOR__ version when you add functionality in a backward compatible manner  and merge changes from `feat/*` into `development`
- update __PATCH__ version when you make backward compatible bug fixes and merge changes from `bugfix/*` into `development`

## automation
- all PRs to `development` automatically add version tags to `development` using semver based on their type of change using [development-merge-semver-tag workflow](.github/workflows/development-merge-semver-tag.yml)
  - `feat/*` or features with non-breaking changes that are not bug fixes increment __MINOR__ in semver vMAJOR.MINOR.PATCH i.e. `v1.0.1` would be incremented to `v1.1.0` in __MINOR__ from a feature
  - `bugfix/*` or bugfix branches increment __PATCH__ version i.e. `v1.0.0`	→ `v1.0.1`
  - features with breaking changes increment __MAJOR__ VERSION i.e. `v1.0.1` → `v2.0.0`

- once the team is ready to release from `development` into an environment automation can release into temporary release branches that push changes up to `env_*` branches for deployment
- the [development-release-to-env workflow](.github/workflows/development-release-to-env.yml) for this is manually triggered
- when manually triggered the user enters the version number to indicate what should be released i.e. `v1.1.123`

## config/setup to make workflows behave correctly
in github settings → actions:
Choose whether GitHub Actions can create pull requests or submit approving pull request reviews.
- Allow GitHub Actions to create and approve pull requests → allow ✅

## todo
- generate github release pages in the UI based on versions pushed into environments (through automation workflows)
- add tag automation for breaking changes __MAJOR__