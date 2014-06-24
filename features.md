# Features

Best practices for creating [Features](http://drupal.org/project/features).

1. **Group related features into packages.** Use packages to organize individual features into groups by site or product on the "Modules" and "Manage features" pages. This can be done via the Features GUI or manually [in your .info files](https://drupal.org/node/542202#package). Accomplish similar organization on the filesystem by prefixing related feature's machine names with a namespace. For example, site-specific features in the "My Awesome Website" package might include `mawblog` (My Awesome Website: Blog) and `mawgallery` (My Awesome Website: Gallery).

1. **Observe general [best practices for naming Drupal projects](projects.md#naming-drupal-projects).**

1. **Keep features in `sites/*/modules/custom` or `sites/*/modules/contrib`.** Some have suggested putting features in `sites/*/modules/features`, but at the end of the day, features are just custom or contributed modules, and confusing this simple distinction has undesirable consequences. For example, when checking for available updates to installed modules, Drupal knows to exclude modules in `sites/*/modules/custom`. If you put your custom features anywhere else, you'll have to exclude them yourself with a [`hook_update_projects_alter()`](https://api.drupal.org/api/drupal/modules!update!update.api.php/function/hook_update_projects_alter/7) implementation.

1. **Don’t cram too much into a feature.**
Features are a great tool for packaging exportable code.  However, when you cram too much in they can become difficult to maintain. Also overloaded features can create some nasty circular dependencies.

1. **Features require code review too.**
Features are a great tool for packaging exportable code.  Often site builders think that since features are exportable code they do not require code review.  Drupal is building your code it obviously knows right?  The problem is that you should always understand what is being checked into code.  Sometimes Drupal Features tries to be too smart for it’s own good and adds unintended items and dependencies to your features. 

1. **Features must be able to deploy into a site without showing an overridden state.**  
The overridden state on a feature identifies a conflict between a features code and the version of the code stored in the DB.  This inconsistency means our site is in an unknown state.  In order for our site to work as expected we need to ensure our site is in a known state.  Getting to a default feature state may require a `drush features-revert all`. This command will revert all the features in your site.  NOTE don’t run that command unless you are sure all your changes are stored in code and are under version control.  

1. **Be careful when adding environment specific variables to a module.**
If you code production values into a feature when you revert that feature in a development environment it may have unexpected consequences.  If you use strong-arm to add variables to a feature just be sure to ask yourself will that variable remain the same in both dev AND prod.  The following are examples of variables that might differ between environments: solr servers, api connection strings, feed urls, etc.  A more appropriate place to store these settings might be either in settings.php or in a module that uses an environment variable/setting.php variable to detect which variable to set. 

1. **Beware of exporting items with IDs.** 
Features makes it really, really easy to export a lot from your site, and that’s awesome.  However, often it will export db IDs.  The problem is that those IDs are often specific to a DB. Your DB and my DB often have different IDs for the same thing.  Some examples are NID(Node ID) and VID(Vocabulary ID). A good workaround in these cases would be to use the [‘UUID’](https://www.drupal.org/project/uuid) module.  [UUID] (http://en.wikipedia.org/wiki/Universally_unique_identifier)s are globally unique IDs.  It allows you to key off a UUID instead of a DB ID. This module has integration for Views, Token, Rules and provides some CTools plugins.

1. **Taxonomy/Blocks/Nodequeus are not exportable by default.**
See (Features Extras) [https://www.drupal.org/project/features_extra] it allows you to export these items as faux-exportables.    It also integrates with the [UUID module] (https://www.drupal.org/project/uuid).  


