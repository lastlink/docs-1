# Schema Guide
This page will give an overview of the proprietary Directus tables that are included in each install. The purpose of these tables is simple – to decouple all Directus proprietary information from your data. This means that at any point you can delete the "directus_" tables and be left with a _pure_ database (schema and data) of your design.

### Your Tables & Fields
The fundamental purpose of Directus is to allow developers to design and create schemas specifically around the needs of their project's scale, performance, architecture, and extensibility. While Directus tries to make no assumptions about your data, there are a few standards which (as of now) should be followed when creating new Tables and Fields:

* `id` – Currently Directus assumes an `id` field as the Primary Key.
* `active` – "Active" is the default name for the status field. [Learn More](/02-user-guide/02-item-listing.md#active-inactive--delete) or [Configure](/04-developer/03-configuration.md#apiconfigurationphp)
* `sort` – "Sort" is the default field name for storing drag-and-drop reordering values. [Learn More](/02-user-guide/02-item-listing.md#reordering)

###`directus_activity`

###`directus_bookmarks`
This table stores all of the left-nav bookmarks for Directus. This includes bookmarks that users create as well as the "System" bookmarks at the bottom. Each record is assigned to a specific user.

* `user` - [Directus user id] This assigns the bookmark to a specific user (there's a ticket to allow for "global" bookmarks using `NULL`)
* `title` - The text to display in the navigation menu
* `url` - The path to navigate to when clicked, relative to the Directus root
* `icon_class` - Deprecated
* `section` - ["search" or "other"] Which nav section to show the link within. User generated bookmarks use "search", while all system links go within "other"

###`directus_columns`

###`directus_files`

###`directus_groups`


###`directus_messages`

###`directus_messages_recipients`

###`directus_preferences`

###`directus_privileges`
Each row on this table is associated with a table (`table_name`) and a Directus user group (`group_id`). Optionally, you can increase the fidelity of your privileges by setting the `status_id` to a an allowed status integer. For instance, you can define a user-group's view privileges for a table specifically  when the _status_ of a record is in draft mode. This might be useful if you'd like your "intern" user-group to only see draft content (not live/published).

The `read_field_blacklist` functions by omitting the given column from the database schema which the API yields, such that the front-end app has no awareness of this column. The `write_field_blacklist` prevents that user group from writing to this column.

The `nav_listed` boolean is used to hide certain tables from the Directus sidebar and table listing. In certain cases you may want records to be visible throughout the CMS (relationally or otherwise) but you don't need that table listed prominently otherwise. You can also use `directus_groups.nav_override` to achieve similar results, but for simply hiding a few tables that might be overkill.

The allow_[permission] columns determine which operations the group may perform on this table. Possible values are: `0` (not allowed), `1` (allowed for content you created), `2` (allowed for content anyone created). To differentiate between who created content (and take advantage of these granular privileges), you must set `directus_tables.user_create_column` to the field within that table which will track the Directus User-ID of the creator.
* `allow_view` - [0,1,**2**] The ability to view a table. Without this permission, the table will be completely omitted from the schema of users in this group.
* `allow_add` - [0,**1**] The ability to add new items to this table. A value of `2` is not an option since you can't _create_ someone else's content.
* `allow_edit` - [0,1,**2**] The ability to edit items from this table.
* `allow_delete` - [0,1,**2**] The ability to delete items from this table. 
* `allow_alter` - [0,**1**] The ability to modify the table's schema.

###`directus_schema_migrations`

###`directus_settings`

###`directus_tables`

###`directus_ui`

###`directus_users`
All the users, including admins, are added within this table. Each user is assigned to a single User Group (`directus_groups`), and that group determines the privileges (`directus_privileges`) for all of its users. 

* `active` - [Directus user id] This 
* `active` - [Directus user id] This 
* `active` - [Directus user id] This 
* `active` - [Directus user id] This 
* `active` - [Directus user id] This 
* `active` - [Directus user id] This 
* `active` - [Directus user id] This 
* `active` - [Directus user id] This 

#### Manually Setting Passwords
If you need to manually reset a user's password directly in the database you can use the following SQL snippet (remember to update the ID of the user to update):

```
UPDATE `directus_users` 
SET `salt` = SHA1(RAND()), `password` = SHA1(CONCAT(salt, 'new-password-here'))
WHERE `id` = '1' 
```
