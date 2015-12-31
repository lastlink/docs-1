#FAQ

### Server Error: Automatically populating $http_raw_post_data is deprecated
Within PHP 5.6.x `$HTTP_RAW_POST_DATA` is deprecated, but sometimes isn't on individual installs (php bug bug#66763)

----------

To solve this add/use/update this on your php.ini
`always_populate_raw_post_data = -1`

### Server error occured!
If you get "Server error occured!" the first time you try to login, it likely means that you missconfigured Apache2. Try adding *overrideAllow All* into your virtualHost.

----------

### How to Enable `mod_rewrite`

#### Unix (MAMP)
1. In the terminal run `a2enmod rewrite`
2. Restart *apache2* with `/etc/init.d/apache2 restart` or `service apache2 restart`

#### Windows (WAMP)

1. `wamp tray icon > apache > apache module > rewrite_module`
