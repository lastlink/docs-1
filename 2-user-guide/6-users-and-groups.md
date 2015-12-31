# Users and Groups
The access control layer was built in response to the need to maintain the privacy and integrity of certain pieces of data within the database, as managed by Directus. This functionality allows Directus administrators to prevent certain groups from reading and writing to specific fields, and from performing certain operations on given tables. 

----------

### Access Control List (ACL)
* `allow_view` - The ability to view a table. Without this permission, the table will be completely omitted from the schema of users in this group.
  * **Off** – Can not view any items in this table or the table itself
  * **User** – Can view items I created in the table
  * **All** – Can view all items in the table (Default)
* `allow_add` - The ability to add new items to this table. A value of `2` is not an option since you can't _create_ someone else's content.
  * **Off** – Can add new items to this table
  * **On** – Can not add new items to this table (Default)
* `allow_edit` - The ability to edit items from this table
  * **Off** – Can not view this table
  * **User** – Can view items I created in the table
  * **All** – Can view all items in the table (Default)
* `allow_delete` - The ability to delete items from this table. 
  * **Off** – Can not delete any items in this table
  * **User** – Can delete items I created in the table
  * **All** – Can delete all items in the table (Default)
* `allow_alter` - The ability to modify the table's schema.
  * **Off** – Can not alter this table
  * **On** – Can alter this table (Default)

----------

### IP Whitelist
If turned on for a user-group, those users will only be able to connect to Directus when accessing over specific IP addresses. This is useful for ensuring a group of users can’t access the system from personal, public, or insecure networks/computers.
