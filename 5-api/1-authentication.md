# Authentication

Authentication privileges follow the user-group that the key was generated from. There are two levels of Authentication:

### API Key
A single consumer-key is generated for each user which is passed as a parameter with every API resource that uses this type. **Used with all GET Resources**

### OAuth
A consumer-key and secret is generated for each user utilizing a regular OAuth flow to acquire OAuth Tokens for use with all requests of this type. **Used with all POST/PUT Resources**

### Security
*All API calls pass through ACL.*

#### Passwords
Directus generates random salts when a password is hashed, encodes the hash-type, salt and stretching iteration count into the “hash encoding string”. During the comparison, it reads this string to retrieve necessary information.

* `CRYPT_BLOWFISH` for passwords
* 8 iteration password stretching
* `/dev/urandom` for randomness
* 128 bit encryption key

#### Database Security
* Prepared statements (PDO) for all database interactions
* Zend-db module for out-of-the-box security

#### Timing Attacks
While account email probing is theoretically possible, you can dummy salt so consistent response time if desired.

#### Password Reset
When a new password is requested, the existing password is NULLified and a new unique password token is sent to the account's email address.

#### XSS
While internal XSS may be possible, successfully authenticated users are assumed to be non-malicious. This was a design decision to give full control to any connected applications. All malicious data needs to be sanitized in the web-application/data entry point, else the database and therefore Directus could become compromised.

#### Session Hijacking
Currently, nothing is done to minimize potential attacks via session hijacking. One possible advancement would be to validate the session with request metadata to provide partial security.

# Custom Endpoints
To add custom endpoints into Directus, simply create new sandboxed endpoints using Slim routes for any custom files.
