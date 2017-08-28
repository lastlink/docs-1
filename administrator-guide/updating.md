# Versions & Updating

> **Note:** Only Administrators have access to these pages and settings.

Below is the process for manually updating Directus. Directus Hosted Instances are automatically updated.

### 1. Backup your database:
  In addition to scheduled backups, you should always create another complete database backup directly before making any broad CMS/database changes.

### 2. Get Directus:

Download and unzip the newest Directus package from the [release list](https://github.com/directus/directus/releases).

> **Note:** Developers who installed Directus by cloning the git repository directly to their server can simply `pull` the newest stable version. Typically this is as simple as navigating to the Directus folder and running: `git pull origin build`

### 3. Replace Files:

If you are not using git, and you are copying and pasting the downloaded files, make sure the new directus files doesn't remove or replace your `/api/config.php` and `/api/configuration.php` files or any custom files you have added into `storage` or `customs` directories.


### 4. Upgrade database:

Run the migration script to update your database/schema by running the command below:

```
$ bin/directus db:upgrade
```
  
**Note:** Make sure to upgrade the composer dependencies, if needed.
