# Upgrading

### Step by Step

Below is the process for manually updating Directus. Directus Hosted Instances are automatically updated.

1. **Backup your database**: In addition to scheduled backups, you should always create another complete database backup directly before making any broad CMS/database changes
2. Download and unzip the newest Directus package from [here](https://github.com/directus/directus/tree/build)
3. Ensuring you don't replace your `/api/config.php` and `/api/configuration.php` files, overwrite your previous version of Directus with the new files
4. Run the migration script to update your database/schema (@TODO)


> Developers who installed Directus by cloning the git repository directly to their server can simply `pull` the newest stable version. Typically this is as simple as navigating to the Directus folder and running: `git pull origin build`
