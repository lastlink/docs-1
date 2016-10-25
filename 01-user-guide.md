# User Guide

----------

## Login
If you attempt to access Directus without being authenticated, you will be directed to the login page. Once successfully logged in, if you were initially following a link to a certain page you will be redirected there – otherwise you'll be taken to the last page you visited within Directus.

> **Developer Note:** That the Directus version is displayed in the bottom-left corner of the login screen. Hovering over the version will reveal the exact git commit hash of your version.

### Forgot Password
Directus always salts and securely encrypts your password, so no one, not even admins, can see your actual password in plain-text. Therefore no one can tell you what your password is – if forgotten, it must be reset. To reset your password, navigate to the login page, fill in your email address, and click the "?" within the password input. You will receive an email with a link to reset your password that is valid for a short period of time.

### Logging Out
It's a good habit to log out of Directus when not actively using it – especially on public computers/devices. The logout button is always available at the bottom of the sidebar, beside your user avatar. Administrators of your system may choose to set an Auto Logout Duration for idle users – by default this is set to 1 hour.

> **Security Note:** Leaving your computer awake and unattended while your Directus user is logged-in could result in a security breach.

----------

## Tables
This straightforward page gives a listing of all tables your user has access to see. For ease of access, tables are listed directly in the Directus sidebar, so you will rarely need to visit this page. To manage a new database table within Directus, an admin must first add it to Directus and a user-group's privileges. If you think a table is missing, contact one of your Instance administrators.

----------

## Item Listing
This is one of the more useful and data-rich pages within Directus. It provides a tabular listing of all the items (records) within the selected table. Clicking the (+) at the top of the page will create a new item in this table, or click on any of the listed items to view/edit it. Beyond this basic functionality, there are also these other features covered below:

### Filtering
The “Add Filter” dropdown will add inputs for searching/filtering within specific fields. Each filter you add is considered an “AND” (not "OR") – for example, with the filters `title="Happy"` and `location="New York"` items would have to match (contain) both. There are several input types for filters: date-chooser, checkbox, dropdown, auto-complete, and the default text-box. Clicking the “×” inside the input will remove that filter.

### Active, Inactive, & Delete
For tables that contain a _Status_ column (Directus uses `active` by default), when selecting items from the listing page you will have the option to change their active status:
* **Active** – These items are considered live/published. A value of "1" is saved.
* **Draft** – Items in draft mode are grayed out visually and this column is saved with a value of 2. Applications should exclude these items from production viewing.
* **Delete** – This effectively removes items from Directus. Though no longer visible, due to the soft delete policy items are maintained within the database with an active value of 0. Applications should exclude these items from production viewing.

Additionally, there is a dropdown in the header for choosing which item's are visible based on status. The options here are:

* **View All** – Shows Active and Draft items. _While deleted items may still exist they are never shown in Directus._
* **View Active** – Shows Active items only
* **View Draft** – Shows Draft items only

> **Developer Note:** Remember to respect the above statuses by only fetching active items (active=1) in your product's data queries. Updating the config file to change the default _Status_ field name, allowed values, and colors.

### Changing Visible Columns
By default the item listing page shows the first few columns of data for any given table. Users can then adjust which columns they see by hovering over the gray table header and clicking the gear on the right – in the dropdown that opens, choose up to eight (8) fields to show. Due to their complexity, many-to-many fields such as the Slideshow UI can not be shown.

### Sorting
As is the case with most tabular data, clicking column headers will sort the data by that field. Clicking a column again will reverse the sort direction – clicking a third time will remove sorting reverting to the default: date created. This is automatically saved on a per user basis and is persistent until changed.

### Reordering
While sorting simply changes the current view of the items, reordering actually _saves_ the order within each item. For tables that contain a “sort” column, items will automatically show a handle on the left side of their row and become re-orderable through drag-and-drop.

> **Note:** While reordering is an excellent way to curate the order of items, you can not drag-and-drop between pages. One work-around is to increase the Items Per Page variable – but it is not advisable to reorder very large datasets in this way.

### Bookmarks
After setting up all of the above options (Filters, View Status, Visible Columns, Sorting) you may want to save it for later use. To save your current layout: simply click the "Add Bookmark" link within the sidebar and give it a name – it will then appear in the Bookmarks section (for your user). To delete a Bookmark, click the "×" beside it's name in the sidebar.

### Bulk Edit
When selecting multiple item checkboxes, a toolbar option for “Batch Editing” will appear. Clicking into this mode will take you to a blank edit page where edits can be made. On this page, clicking “edit” for a particular field indicates that Directus should save that value for _all_ selected items.

> **Caution:** Use this feature with care as it is easy to overwrite a large amount of items.

### Footer
For certain columnar data (eg: Integers), a footer will show at the bottom of the table with additional calculated information:
    * **SUM** – Adds up all column values from each visible item
    * **MIN** – Shows the lowest column value within all visible items
    * **MAX** – Shows the highest column value within all visible items
    * **AVG** – Shows the average of all column values within all visible items

----------

## Create & Edit
These pages display all the fields the current user has permission to view. Admins can change the field order, interface type, and field notes within _Settings > Tables & Inputs_. If your project would benefit from proprietary or otherwise custom data interfaces, it's easy to extend our Core interfaces or create new ones – there are no limits to what you can create!

### Saving
Once you've added or edited data on the page, you'll probably want to save those changes. As with other Directus pages, the (✓) button at the top of the screen will both save and return you to the listing. On this page however, to the right of the primary button there's an additional triangle dropdown providing three additional options:

* **Save** – (Primary action button) Saves changes and returns you to the item listing page
* **Save and Stay** – Saves changes and keeps you on the edit page
* **Save as Copy** – Saves the current item (with changes) as a _new_ item, the original item you opened is unchanged.
* **Save and Add** – Saves changes and takes you to a blank new item page for that table. This option can be useful when repetatively adding items.

### Item Comments
In addition to a full messaging system, you can also leave comments on individual items from their detail page. For example, you could let the other users know that the item still needs to be reviewed before going live – or reference specific users with the "@" character. When referenced in comments, users will receive a Directus notification and, if set within their preferences, an accompanying email.

### Revision History
Every change made by users within Directus is tracked to give comprehensive accountability. The user, their IP address and user-agent, the date/time of the change, any effected data (delta), and a _complete_ item backup are all saved for each and every edit. You can see a history of these changes at the bottom of this item detail page – commingled chronologically with any item comments.

----------

## Files
This page provides a listing of _all_ files uploaded through the Directus system, it also includes any videos or embeds (eg: _YouTube_, _Vimeo_) that have been linked. 

### Metadata
**IPTC** – (_location, caption, keywords_) is extracted from the files when they're uploaded and automatically stored with each file.

### Custom Fields
You can add as many additional custom fields to `directus_files` as you'd like. 

## Messages
There are two types of messages within Directus:

### Item Comments
Every item within the system can contain comments attached within the Item History for associating specific feedback.

### User Messages
Similar to email, users can send messages to other Directus users. An option exists to have all Messages forwarded to your email address.

----------

## Users & Groups
You need to authenticate (log in) as a user to access data through Directus or its API. Each user is assigned to a user-group which defines it's access privileges with Directus. When you install Directus your first user is in the admin group – the highest level possible – with unrestricted data access, the ability to create and edit users, and access to the [Settings](/03-interfaces) area.

Each user is organized by group on the listing page and has the following default fields for storing information:

* **First Name** – The user's first name
* **Last Name** – The user's last name
* **Email** –  The user's email address (used to log in)
* **Email Messages** – A checkbox for if Directus messages should be forwarded to the above email address
* **Password** – The user's password (used to log in)
  * This is encrypted in the database – no one can see your actual password or tell it to you
* **Group** – The permission group for the user – only admins can create new Groups [Learn More](/04-developer/05-privileges-and-access.md)
* **Position** – The user's job title or role
* **Phone** – The user's primary phone number (other fields can be added to store additional numbers)
* **Location** – The user's primary location, or the office the user belongs to
* **Avatar** – The user's image used throughout Directus, by default this is pulled from Gravatar
* **Address** – The user's address
* **City** –  The user's city
* **State** –  The user's state
* **Zip** –  The user's zip code

> **Note:** Adding additional custom fields to the users table is a great way to quickly create a company directory.

### IP Whitelist
If turned on for a user-group, those users will only be able to connect to Directus when accessing over specific IP addresses. This is useful for ensuring a group of users can’t access the system from personal, public, or insecure networks/computers.
