#FAQ

### Server Error: Automatically populating $http_raw_post_data is deprecated
Within PHP 5.6.x `$HTTP_RAW_POST_DATA` is deprecated, but sometimes isn't on individual installs (php bug bug#66763)

To solve this add/use/update this on your php.ini
`always_populate_raw_post_data = -1`
