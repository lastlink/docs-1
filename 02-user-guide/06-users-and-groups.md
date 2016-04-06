# Users & Groups
You need to authenticate (log in) as a user to access data through Directus or its API. Each user is assigned to a user-group which defines it's access privileges with Directus. When you install Directus your first user is in the admin group – the highest level possible – with unrestricted data access, the ability to create and edit users, and access to the [Settings](/03-interfaces) area.

Each user is organized by group on the listing page and has the following default fields for storing information:

* **First Name** – The user's first name
* **Last Name** – The user's last name
* **Email** –  The user's email address (used to log in)
* **Email Messages** – A checkbox for if Directus messages should be forwarded to the above email address
* **Password** – The user's password (used to log in)
  * This is encrypted in the database – no one can see your actual password or tell it to you
* **Group** – The permission group for the user – only admins can create new Groups [Learn More](https://github.com/directus/docs/blob/master/3-developer/3-privileges-and-access-control.md)
* **Position** – The user's job title or role
* **Phone** – The user's primary phone number (other fields can be added to store additional numbers)
* **Location** – The user's primary location, or the office the user belongs to
* **Avatar** – The user's image used throughout Directus, by default this is pulled from Gravatar
* **Address** – The user's address
* **City** –  The user's city
* **State** –  The user's state
* **Zip** –  The user's zip code

> **Note:** Adding additional custom fields to the users table is a great way to quickly create a company directory.

----------

### IP Whitelist
If turned on for a user-group, those users will only be able to connect to Directus when accessing over specific IP addresses. This is useful for ensuring a group of users can’t access the system from personal, public, or insecure networks/computers.
