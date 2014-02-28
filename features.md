# Features

Best practices for creating [Features](http://drupal.org/project/features).

1. **Group related features into packages.** Use packages to organize individual features into groups by site or product on the "Modules" and "Manage features" pages. This can be done via the Features GUI or manually [in your .info files](https://drupal.org/node/542202#package). Accomplish similar organization on the filesystem by prefixing related feature's machine names with a namespace. For example, site-specific features in the "My Awesome Website" package might include `mawblog` (My Awesome Website: Blog) and `mawgallery` (My Awesome Website: Gallery).

1. **Observe general [best practices for naming Drupal projects](projects.md#naming-drupal-projects).**

1. **Keep features in `sites/*/modules/custom` or `sites/*/modules/contrib`.** Some have suggested putting features in `sites/*/modules/features`, but at the end of the day, features are just custom or contributed modules, and confusing this simple distinction has undesirable consequences. For example, when checking for available updates to installed modules, Drupal knows to exclude modules in `sites/*/modules/custom`. If you put your custom features anywhere else, you'll have to exclude them yourself with a [`hook_update_projects_alter()`](https://api.drupal.org/api/drupal/modules!update!update.api.php/function/hook_update_projects_alter/7) implementation.
