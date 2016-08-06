# Installation

### Server Preparation
1. Check that your server meets the [requirements](/01-getting-started/02-requirements.md)
2. Download and unzip the Directus package from [here](https://github.com/directus/directus/tree/build)
3. Create a database and MySQL user with access/modify privileges on your server
  * You can also use an existing database, but it's worth taking a look at the typical [Directus Schema](/04-developer/06-schema-guide.md)
4. Upload the files to a public directory on your server
5. Run the installation script by accessing the URL where you uploaded the files

----------

### Installation Walkthrogh

#### Step 0 – Requeriments
The pre-installation step, it will only be shown if a requirements wasn't found.

#### Step 1 – Project Info
* _Project Name_ – The name of this project
* _Project Path_ – This should auto-fill, but it's the path of this install
* _Admin Email_ – The email address for your first Directus user/admin
* _Admin Password / Confirm_ – The password for your first Directus user/admin

#### Step 2 – Database
* _Database Type_ – The Database type to be used. (Only MySQL is supported, including MariaDB, Percona Server or equivalent). _SQLite and PostgreSQL support are under Development at the moment_
* _Host Name_ – The database host, Typically `localhost`.
* _Host Port_ - The database host port.
* _Username_ – The database user with access and modify privileges.
* _Password_ – The password for that database user.
* _Database Name_ – The name of an existing database to be managed.
* _Install Schema_ – List of boilerplate schemas to be imported.

#### Step 3 – Confirmation
* If the database connection succeeds you'll be shown an installation summary page and given an opportunity to email these details to the admin user.

> **Security Note:** Once you have completed the install, make sure to delete install folder.

----------

### Troubleshooting
If you're having problems with your Directus install, please visit our [troubleshooting section](/05-troubleshooting).

* [Server error occured!](#)
* [Enable mod_rewrite](/05-troubleshooting)
