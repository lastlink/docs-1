# Simple Installation

## Requirements
Directus is a forward-looking framework and therefore may not support certain legacy systems. If your server is not compatible with the requirements below, please contact your host to upgrade.

* Apache HTTP Server
* mod_rewrite ([help](/05-troubleshooting/01-faq.md))
* PHP 5.5+
  * curl
  * gd
  * finfo
  * pdo_mysql
  * mcrypt
* MySQL 5.2+

> **Optional Enhancement:** Installing *Imagick* adds thumbnail support for TIFF, PSD, and PDF files

## Server Preparation
1. Check that your server meets the [requirements](/01-getting-started/02-installation.md#requirements)
2. Download and unzip the Directus package from [here](https://github.com/directus/directus/tree/build)
3. Create a database and MySQL user with access/modify privileges on your server.
4. Upload the files to a public directory on your server
5. Run the installation script by accessing the URL where you uploaded the files

> **Existing Databases:** You can also use an existing database, but should look at the typical [Directus Schema](/04-developer/06-schema-guide.md)

## Installation Wizard
A pre-installation check will run but will only be shown if the server requirements are not met.

### Step 1 – Project Info
* _Project Name_ – The name of this project
* _Project Path_ – This should auto-fill, but it's the path of this install
* _Admin Email_ – The email address for your first Directus user/admin
* _Admin Password / Confirm_ – The password for your first Directus user/admin

### Step 2 – Database
* _Database Type_ – The database type to be used. (Only MySQL is supported, including MariaDB, Percona Server or equivalent).
* _Host Name_ – The database host, typically `localhost`
* _Host Port_ - The database host port
* _Username_ – The database user with access and modify privileges
* _Password_ – The password for that database user
* _Database Name_ – The name of an existing database to be managed
* _Install Schema_ – List of optional boilerplate schemas

> **Other Database Types:** SQLite, PostgreSQL, and MongoDB support are in development

### Step 3 – Confirmation
* If the database connection succeeds you'll be shown an installation summary page and given an opportunity to email these details to the admin user.

> **Security Note:** Once you have completed the install, make sure to delete install folder.

### Troubleshooting
If you're having problems with your Directus install, please visit our [troubleshooting section](/05-troubleshooting).
