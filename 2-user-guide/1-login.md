# Login
If you attempt to access Directus without being authenticated, you will be directed to the login page. Once successfully logged in, if you were initially following a link to a certain page you will be redirected there – otherwise you'll be taken to the last page you visited within Directus.

> **Developer Note:** That the Directus version is displayed in the bottom-left corner of the login screen. Hovering over the version will reveal the exact git commit hash of your version.

----------

### Forgot Password
Directus always salts and securely encrypts your password, so no one, not even admins, can see your actual password in plain-text. Therefore no one can tell you what your password is – if forgotten, it must be reset. To reset your password, navigate to the login page, fill in your email address, and click the "?" within the password input. You will receive an email with a link to reset your password that is valid for a short period of time.

----------

### Logging Out
It's a good habit to log out of Directus when not actively using it – especially on public computers/devices. The logout button is always available at the bottom of the sidebar, beside your user avatar. Administrators of your system may choose to set an Auto Logout Duration for idle users – by default this is set to 1 hour.

> **Security Note:** Leaving your computer awake and unattended while your Directus user is logged-in could result in a security breach.
