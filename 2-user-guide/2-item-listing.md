# Item Listing
This is one of the more useful and data-rich pages within Directus. It provides a tabular listing of all the items (records) within the selected table. Clicking the (+) at the top of the page will create a new item in this table, or click on any of the listed items to view/edit it. Beyond this basic functionality, there are also these other features covered below:


### Filtering
The “Add Filter” dropdown will add inputs for searching/filtering within specific fields. Each filter you add is considered an “AND” (not "OR") – for example, with the filters `title="Happy"` and `location="New York"` items would have to match (contain) both. There are several input types for filters: date-chooser, checkbox, dropdown, auto-complete, and the default text-box. Clicking the “×” inside the input will remove that filter.

### Active, Inactive, & Delete
For tables that contain a _Status_ column (Directus uses `active` by default), when selecting items from the listing page you will have the option to change their active status:
* **Active** – These items are considered live/published. A value of "1" is saved.
* **Draft** – Items in draft mode are grayed out visually and this column is saved with a value of 2. Applications should exclude these items from production viewing.
* **Delete** – This effectively removes items from Directus. Though no longer visible, due to the soft delete policy items are maintained within the database with an active value of 0. Applications should exclude these items from production viewing.

> Developer Note: Remember to respect the above statuses by only fetching active items (active=1) in your product's data queries. Updating the config file to change the default _Status_ field name, allowed values, and colors.

### Changing Visible Columns
By default Directus shows the first few columns of data for any given table. Users can then adjust which columns they see by hovering over the gray table header and selecting the gear on the right.

### Sorting
As is the case with most tabular data, clicking column headers will sort the data by that field. Clicking a column again will reverse the sort direction – clicking a third time will remove sorting reverting to the default: date created. This is automatically saved on a per user basis and is persistent until changed.

### Snapshots
As with most datasets, sometimes there are multiple specific views for any given dataset. To save your current layout, simply click the snapshot button from within the toolbar and it will be added to the sidebar for your user. Snapshots save the following parameters: filters, sort column and direction, visible columns, and visible active states

### Reordering
For tables that contain a “sort” column, items will automatically show a handle on the left side of the listing page and become re-orderable through drag-and-drop.

### Bulk Edit
Selecting more than one item with the left checkboxes will give a toolbar option for “Batch Editing”. Clicking into this mode will take you to a blank edit page where edits can be made. On this page, clicking “edit” for a particular field indicates that Directus should save that value for all chosen items.

### Bookmarking
For databases that contain a large number of tables, instead of the sidebar listing all tables, Directus can be setup to only show user bookmarked tables (individual user preference). Tables are bookmarked by clicking the star at the top of the item listing page.

### Footer
For certain columnar data (eg: Integers), a footer will show additional calculated information.:
    * **SUM** Adds up all column values from each visible item
    * **MIN** Shows the lowest column value within all visible items
    * **MAX** Shows the highest column value within all visible items
    * **AVG** Shows the average of all column values within all visible items
