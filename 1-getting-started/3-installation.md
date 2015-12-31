# Installation

### Server Preparation
1. Check that your server meets the [requirements](docs/1-getting-started/2-requirements.md)
2. Download and unzip the Directus package from [here](https://github.com/directus/directus/tree/build)
3. Create a database and MySQL user with access/modify privileges on your web server
  * You can also use an existing database, but it's worth taking a look at the typical [Directus Schema](docs/3-developer/4-schema-guide.md)
4. Upload the files to a public directory within your web-server
5. Run the Directus installation script by accessing the URL where you uploaded the files

----------

### Installation Walkthrogh
1. **Project Info**
  * _Project Name_ – The name of this project
  * _Project Path_ – This should auto-fill, but it's the path of this install
  * _Admin Email_ – The email address for your first Directus user/admin
  * _Admin Password / Confirm_ – The password for your first Directus user/admin
2. **Database**
  * _Host Name_ – Typically `localhost`
  * _Username_ – MySQL user with access and modify privileges
  * _Password_ – The password for that MySQL user
  * _Database Name_ – The name of the new or existing database to be managed
  * _Install Sample Data_ – Check this to import the example schema
3. **Confirmation**
  * If the database connection succeeds you'll be shown an installation summary page and given an opportunity to email these details to the admin user.

> Once you have completed the install, make sure to delete install folder for security purposes.

----------

### Troubleshooting
If you're having problems with your Directus install, please visit our [troubleshooting section](docs/4-troubleshooting/).

* [Server error occured!](#)
* [Enable mod_rewrite](docs/4-troubleshooting/enable_mod_rewrite.md)
