# test-branching-strategies

## branches
- `feat/f-###` feature branches branched from `development` to PR back to `development` once complete
- `bugfux/b-###` bugfix branches branched from `development` to PR back to `development` once complete
- `development` used as development branch PRs from feature `feat/` or bugfix `bugfix/` branches target `development`
- `master` branch holds up to date versions of code?
- release branches PRs from `development` to release branches `release/VERSION_TAG` target deployment to these branches:
  - `env_test`
  - `env_uat`
  - `env_prod`

## semver tagging strategy
refer to [semver](https://semver.org/)
- update MAJOR version when you make incompatible API changes
- update MINOR version when you add functionality in a backward compatible manner  and merge changes from `feat/*` into `development`
- update PATCH version when you make backward compatible bug fixes and merge changes from `bugfix/*` into `development

## automation
- all PRs to dev automatically add version tags to dev using semver based on their type of change
  - feat/ or features with non breaking changes that are not bug fixes increment MINOR in semver vMAJOR.MINOR.PATCH i.e. v1.0.1 would be incremented to v1.1.0 in PATCH from a feature
  - bugfix/ bugfix branches increment PATCH version i.e. v1.0.0 >> v1.0.1
  - features with breaking changes increment MAJOR VERSION i.e. v1.0.1 >> v2.0.0

- once the team is release ready PRs from development automation can release into temporary release branches that push changes up to `env` branches for deployment
- PRs from `development` to `release` include optional parameters 

## config
in github settings > actions:
Choose whether GitHub Actions can create pull requests or submit approving pull request reviews.
- Allow GitHub Actions to create and approve pull requests >> allow