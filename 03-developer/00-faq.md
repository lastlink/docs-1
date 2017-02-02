#FAQ

### Bug Reporting and Feature Requests
**Report bugs directly on [GitHub Issues](https://github.com/directus/directus/issues/new) – request and vote for new features on [FeatHub](http://feathub.com/directus/directus). For all security related issues, please chat with us directly through [getdirectus.com](http://getdirectus.com/)**

-------------

### Server Error: Automatically populating $http_raw_post_data is deprecated
Within PHP 5.6.x `$HTTP_RAW_POST_DATA` is deprecated, but sometimes isn't on individual installs ([php bug #66763](https://bugs.php.net/bug.php?id=66763))

To solve this add/use/update this on your php.ini
`always_populate_raw_post_data = -1`

### Server error occured!
If you get "Server error occured!" the first time you try to login, it likely means that you missconfigured Apache2. Try adding *AllowOverride All* into your virtualHost.

### MySQL Strict Mode
Directus does not fully support Strict Mode due to limitations with the PDO and MySQL Drivers. Please disable MySQL Strict Mode before installation.

You can check to see if your database is in strict mode with the following queries:
```
SELECT @@GLOBAL.sql_mode;
SELECT @@SESSION.sql_mode;
SHOW VARIABLES LIKE 'sql_mode';
```

### How to Enable `mod_rewrite`

#### Unix
1. In the terminal run `a2enmod rewrite`
2. Restart *apache2* with `/etc/init.d/apache2 restart` or `service apache2 restart`

#### Windows (WAMP)
1. `wamp tray icon > apache > apache module > rewrite_module`

#### Mac (MAMP PRO)
1. Click on `modules` tab.
2. Look for and check `rewrite_module`.

### `mod_rewrite` is enabled and still not working
1. Go to your apache configuration (httpd.conf or apache.conf)
2. Look for the `<Directory>` directive that matches the Directus path.

    Ex:
    ```
    <Directory "/var/www/html">
        AllowOverride All
        Order allow,deny
        Allow from all
    </Directory>
    ```
3. Add `AllowOverride All`, If `AllowOverride None` exists change `None` to `All` to allow `.htaccess` files.

### `mod_rewrite` is enabled and still getting 404 error.

If you are using VirtualDocumentRoot `RewriteBase` needs to be set.

1. Go to `/directus/path/.htaccess` and add `RewriteBase /` just below `RewriteEngine On`.
2. Go to `/directus/path/api/.htaccess` and add `RewriteBase /api` just below `RewriteEngine On`.

### How do I reset a password manually?
[This section](https://github.com/directus/docs/blob/master/04-developer/06-schema-guide.md#manually-setting-passwords) of the Docs explains how to update a password with a SQL command.
