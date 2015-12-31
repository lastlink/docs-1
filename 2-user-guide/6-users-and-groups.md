# Users and Groups
### Access Control List (ACL)
* **View** – Ability to view your items (created by you)
* **BigView** – Ability to create the items of other users
* **Add** – Ability to add new items
* **Edit** – Ability to edit or change your items, including status changes
* **BigEdit** – Same as edit but for other user’s items
* **Delete** – Ability to delete your items – the soft-delete policy enforces that items are removed from Directus but not deleted from the database
* **BigDelete** – Same as delete but for other user’s items
* **Alter** – Permission for making schema level changes such as field order

----------

### IP Whitelist
If turned on for a user-group, those users will only be able to connect to Directus when accessing over specific IP addresses. This is useful for ensuring a group of users can’t access the system from personal, public, or insecure networks/computers.
