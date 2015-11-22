# Item Listing
### Filtering
Choosing a field from the “Add Filter” dropdown will provide an input for quick and easy searching of larger datasets. Each filter is considered an “AND”, limiting results using one of several inputs: date-chooser, checkbox, dropdown, auto-complete, and the default text-box. Clicking the “×” will remove a given filter.

### Active, Inactive, & Delete
For tables that contain an “active” column, when selecting items from the listing page you will have the option to change their active status:
* Active – These items are considered production-ready.
* Draft – Items in draft mode are grayed out visually and this column is saved with a value of 2. Applications should exclude these items from production viewing.
* Delete – This effectively removes items from Directus, though no longer visible, due to the soft delete policy items are maintained within the database with an active value of 0. Applications should exclude these items from production viewing.

You can also override the above with a custom "status" field name, allowed values, and colors. See updating config files.

### Changing Visible Columns
By default Directus shows the first few columns of data for any given table. Users can then adjust which columns they see by hovering over the gray table header and selecting the gear on the right.

### Sorting
As is the case with more tabular data, clicking column headers will allow for the sorting of data by that field. Clicking a column again will reverse the sort direction – clicking a third time will remove sorting reverting to the default: date created. This is automatically saved on a per user basis and is persistent until changed.

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
