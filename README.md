# test-branching-strategies

## branches
- feat/f-### feature branches branched from dev to PR back to dev once complete
- bugfux/b-### bugfix branches branched from dev to PR back to dev once complete
- development used as dev branch PRs from feature branches target dev
- master up to date versions of code
- release branches (PRs from dev to release target deployment to these branches)
  - `env_test`
  - `env_uat`
  - `env_prod`

## semver
MAJOR version when you make incompatible API changes
MINOR version when you add functionality in a backward compatible manner
PATCH version when you make backward compatible bug fixes

## automation
- all PRs to dev automatically add version tags to dev using semver based on their type of change
  - feat/ or features with non breaking changes that are not bug fixes increment MINOR in semver vMAJOR.MINOR.PATCH i.e. v1.0.1 would be incremented to v1.1.0 in PATCH from a feature
  - bugfix/ bugfix branches increment PATCH version i.e. v1.0.0 >> v1.0.1
  - features with breaking changes increment MAJOR VERSION i.e. v1.0.1 >> v2.0.0

- once the team is release ready PRs from development automation can release into temporary release branches that push changes up to `env` branches for deployment
- PRs from `development` to `release` include optional parameters 
