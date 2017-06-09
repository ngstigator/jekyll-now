---
published: true
---
## Why?

Recently I had a project where we needed to switch from a standard Drupal 7 site configuration to use an install profile instead. This was done to facilitate core and contrib updates via [Drush](https://www.drupal.org/project/drush).

## Prerequisites
- an install profile that you wish to switch to
- an existing Drupal 7 site
- Drush is installed on your environment
- [Registry Rebuild](https://www.drupal.org/project/registry_rebuild) is installed on your environment

To set the install profile of the site, simply run `drush vset --exact install_profile {YOUR_INSTALL_PROFILE}`

Then remap modules and themes to use their appropriate analogues in the install profile. Rebuild the registry by running `drush rr`. Now all references to `sites/all/modules` are replaced by `profiles/{YOUR_INSTALL_PROFILE}/modules`.
