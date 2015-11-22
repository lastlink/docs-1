# Requirements
_Directus is a forward-looking framework and therefore may not support certain legacy systems. If your server is not compatible with the requirements below, please contact your host to upgrade._

* Apache HTTP Server
* mod_rewrite
* PHP 5.5+
* curl
* gd
* MySQL 5.2+
* pdo_mysql
* mcrypt

Optionally, you can install the following for added functionality:
* Imagick – _Progressive enhancement adding thumbnail support for TIFF, PSD, and PDF files_

#### How To Enable *Mod_Rewrite*

**Unix (MAMP)**

1. In the terminal run `a2enmod rewrite`
2. Restart *apache2* with `/etc/init.d/apache2 restart` or `service apache2 restart`

**Windows (WAMP)**

1. `wamp tray icon > apache > apache module > rewrite_module`
