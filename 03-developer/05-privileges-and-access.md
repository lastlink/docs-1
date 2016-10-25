# Privileges & Access Control List (ACL)

The access control layer was built in response to the need to maintain the privacy and integrity of certain pieces of data within the database, as managed by Directus. This functionality allows Directus administrators to prevent certain groups from reading and writing to specific fields, and from performing certain operations on given tables. 

### The Basics
Each row within `directus_privileges` determines the table permissions (`table_name`) for a user group (`group_id`). Optionally, you can increase the fidelity of your privileges by setting the `status_id` to a an allowed status integer. For instance, you can define a user-group's view privileges for a table specifically  when the _status_ of a record is in draft mode. This might be useful if you'd like your "intern" user-group to only see draft content (not live/published).

----------

### Field-Level Control
The `read_field_blacklist` functions by omitting the given column from the database schema which the API yields, such that the front-end app has no awareness of this column. The `write_field_blacklist` prevents that user group from writing to this column.

----------

### Navigation
The `nav_listed` boolean is used to hide certain tables from the Directus sidebar and table listing. In certain cases you may want records to be visible throughout the CMS (relationally or otherwise) but you don't need that table listed prominently otherwise. You can also use `directus_groups.nav_override` to achieve similar results, but for simply hiding a few tables that might be overkill.

----------

### Permissions
The allow_[permission] columns determine which operations the group may perform on this table. Possible values are: `0` (not allowed), `1` (allowed for content you created), `2` (allowed for content anyone created). To differentiate between who created content (and take advantage of these granular privileges), you must set `directus_tables.user_create_column` to the field within that table which will track the Directus User-ID of the creator.

#### Access Control List (ACL)
* `allow_view` - The ability to view a table. Without this permission, the table will be completely omitted from the schema of users in this group.
  * ![no-priv](http://getdirectus.com/assets/imgs/docs/no-priv.png) – **Off (`0`)** – Can not view any items in this table or the table itself
  * ![partial-priv](http://getdirectus.com/assets/imgs/docs/partial-priv.png) – **User (`1`)** – Can view items I created in the table
  * ![big-priv](http://getdirectus.com/assets/imgs/docs/big-priv.png) – **All (`2`)** – Can view all items in the table (Default)
* `allow_add` - The ability to add new items to this table. A value of `2` is not an option since you can't _create_ someone else's content.
  * ![no-priv](http://getdirectus.com/assets/imgs/docs/no-priv.png) – **Off (`0`)** – Can add new items to this table
  * ![priv](http://getdirectus.com/assets/imgs/docs/priv.png) – **On (`1`)** – Can not add new items to this table (Default)
* `allow_edit` - The ability to edit items from this table
  * ![no-priv](http://getdirectus.com/assets/imgs/docs/no-priv.png) – **Off (`0`)** – Can not view this table
  * ![partial-priv](http://getdirectus.com/assets/imgs/docs/partial-priv.png) – **User (`1`)** – Can view items I created in the table
  * ![big-priv](http://getdirectus.com/assets/imgs/docs/big-priv.png) – **All (`2`)** – Can view all items in the table (Default)
* `allow_delete` - The ability to delete items from this table. 
  * ![no-priv](http://getdirectus.com/assets/imgs/docs/no-priv.png) – **Off (`0`)** – Can not delete any items in this table
  * ![partial-priv](http://getdirectus.com/assets/imgs/docs/partial-priv.png) – **User (`1`)** – Can delete items I created in the table
  * ![big-priv](http://getdirectus.com/assets/imgs/docs/big-priv.png) – **All (`2`)** – Can delete all items in the table (Default)
* `allow_alter` - The ability to modify the table's schema.
  * ![no-priv](http://getdirectus.com/assets/imgs/docs/no-priv.png) – **Off (`0`)** – Can not alter this table
  * ![priv](http://getdirectus.com/assets/imgs/docs/priv.png) – **On (`1`)** – Can alter this table (Default)
