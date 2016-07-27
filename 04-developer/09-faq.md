#FAQ

### Bug Reporting and Feature Requests
**Report bugs directly on [GitHub Issues](https://github.com/directus/directus/issues/new) – request and vote for new features on [FeatHub](http://feathub.com/directus/directus). For all security related issues, please chat with us directly through [getdirectus.com](http://getdirectus.com/)**

-------------

### Server Error: Automatically populating $http_raw_post_data is deprecated
Within PHP 5.6.x `$HTTP_RAW_POST_DATA` is deprecated, but sometimes isn't on individual installs (php bug bug#66763)

To solve this add/use/update this on your php.ini
`always_populate_raw_post_data = -1`

### Server error occured!
If you get "Server error occured!" the first time you try to login, it likely means that you missconfigured Apache2. Try adding *overrideAllow All* into your virtualHost.

### How to Enable `mod_rewrite`

#### Unix (MAMP)
1. In the terminal run `a2enmod rewrite`
2. Restart *apache2* with `/etc/init.d/apache2 restart` or `service apache2 restart`

#### Windows (WAMP)

1. `wamp tray icon > apache > apache module > rewrite_module`

### How do I reset a password manually?
[This section](https://github.com/directus/docs/blob/master/04-developer/06-schema-guide.md#manually-setting-passwords) of the Docs explains how to update a password with a SQL command.
