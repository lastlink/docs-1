# Directus CLI

Directus CLI is a command-line interface that provide different commands to help you with different task, such as install Directus, change an user email or upgrade your schema to directus most recent schema.

There is a help command that will give you information about the command.

```bash
# this will give you information about the current modules
php bin/directus help
```

To get information of an specific command you can do the following:

```bash
# this will give you information about the **install** modules
php bin/directus help install
```

## Available Modules

## Install Module
Includes commands to install and configure Directus

### Configure Directus:

Creates the `config.php` and `configuration.php` files.

**IMPORTANT:** This command will overwrite the current `config.php` and `configuration.php` files.

```bash
php bin/directus install:config -h <db_host> -n <db_name> -u <db_user> -p <db_pass> -d <directus_path>
```

- db_host - the database host.
- db_name - the database name. _It must exists_.
- db_user - the database user's name.
- db_pass - the database user's password.
- directus_path - (Optional) Directus Path inside the host. If Directus is installed within a subdirectory of the main host, that subdirectory is the <directus_path>.

Ex: http://example.local

```bash
php bin/directus install:config -h localhost -n directus -u root -p pass
```

Ex: http://example.local/directus

```bash
php bin/directus install:config -h localhost -n directus -u root -p pass -d directus
```

### Populate the DB with the schema:

Creates all the Directus core tables. It depends on the configuration files, inside `/api/config.php` and `/api/configuration.php`.

```bash
php bin/directus install:database
```

### Install the initial configurations:

Crete the default Admin user and the site's default settings.

```bash
php bin/directus install:install -e <admin_email> -p <admin_password> -t <site_name>
```

- admin_email - the admin email
- admin_password - the admin password
- site_name - the project title

Ex:
```bash
php bin/directus install:install -e admin@directus.local -p password -t "Directus Example"
```

## User Module
Includes commands to manage Directus users

### Change a user password:

```bash
php bin/directus user:password -e <user_email> -p <new_password>
```

- user_email - the user email
- new_password - the user new password

Ex:

```bash
php bin/directus user:password -e admin@directus.local -p newpassword
```