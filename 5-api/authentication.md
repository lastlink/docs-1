# Authentication

Authentication privileges follow the user-group that the key was generated from. There are two levels of Authentication:

### API Key
A single consumer-key is generated for each user which is passed as a parameter with every API resource that uses this type. **Used with all GET Resources**

### OAuth
A consumer-key and secret is generated for each user utilizing a regular OAuth flow to acquire OAuth Tokens for use with all requests of this type. **Used with all POST/PUT Resources**
