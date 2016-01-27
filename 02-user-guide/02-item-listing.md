# Item Listing
This is one of the more useful and data-rich pages within Directus. It provides a tabular listing of all the items (records) within the selected table. Clicking the (+) at the top of the page will create a new item in this table, or click on any of the listed items to view/edit it. Beyond this basic functionality, there are also these other features covered below:

----------

### Filtering
The “Add Filter” dropdown will add inputs for searching/filtering within specific fields. Each filter you add is considered an “AND” (not "OR") – for example, with the filters `title="Happy"` and `location="New York"` items would have to match (contain) both. There are several input types for filters: date-chooser, checkbox, dropdown, auto-complete, and the default text-box. Clicking the “×” inside the input will remove that filter.

----------

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

----------

### Changing Visible Columns
By default the item listing page shows the first few columns of data for any given table. Users can then adjust which columns they see by hovering over the gray table header and clicking the gear on the right – in the dropdown that opens, choose up to eight (8) fields to show. Due to their complexity, many-to-many fields such as the Slideshow UI can not be shown.

----------

### Sorting
As is the case with most tabular data, clicking column headers will sort the data by that field. Clicking a column again will reverse the sort direction – clicking a third time will remove sorting reverting to the default: date created. This is automatically saved on a per user basis and is persistent until changed.

----------

### Reordering
While sorting simply changes the current view of the items, reordering actually _saves_ the order within each item. For tables that contain a “sort” column, items will automatically show a handle on the left side of their row and become re-orderable through drag-and-drop.

> **Note:** While reordering is an excellent way to curate the order of items, you can not drag-and-drop between pages. One work-around is to increase the Items Per Page variable – but it is not advisable to reorder very large datasets in this way.

----------

### Bookmarks
After setting up all of the above options (Filters, View Status, Visible Columns, Sorting) you may want to save it for later use. To save your current layout: simply click the "Add Bookmark" link within the sidebar and give it a name – it will then appear in the Bookmarks section (for your user). To delete a Bookmark, click the "×" beside it's name in the sidebar.

----------

### Bulk Edit
When selecting multiple item checkboxes, a toolbar option for “Batch Editing” will appear. Clicking into this mode will take you to a blank edit page where edits can be made. On this page, clicking “edit” for a particular field indicates that Directus should save that value for _all_ selected items.

> **Caution:** Use this feature with care as it is easy to overwrite a large amount of items.

----------

### Footer
For certain columnar data (eg: Integers), a footer will show at the bottom of the table with additional calculated information:
    * **SUM** – Adds up all column values from each visible item
    * **MIN** – Shows the lowest column value within all visible items
    * **MAX** – Shows the highest column value within all visible items
    * **AVG** – Shows the average of all column values within all visible items
