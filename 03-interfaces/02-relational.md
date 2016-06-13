# Relational Data

Since SQL is a relational database, Directus has several UIs that can help clearly and easily manage relationships between items. An item can have related items from the same table (eg: *Project -> Related Project*) or a different table (eg: *Project -> Category*). An item can also have relationships to a single item (eg: *Shirt -> Size*) in a Many-to-One (or One-to-Many) relationship, or to multiple items (eg *Shirt -> Materials*) through Many-to-Many relationships.

#### Many-to-One (M2O)
Many-to-One relationships save the `id` from another item as it's value, creating a dynamic relationship to that item.

#### Many-to-Many (M2M)
Many-to-Many relationships are quite a bit more complex, but very powerful. There are two things that are important to understand for M2Ms: Junction Tables, and Aliases. Let's use our *Shirt -> Materials* example from before to explore how this works:

```
shirt (Table)
* id
* name
* size
* "materials" (M2M Alias)

materials (Table)
* id
* material

shirt_materials (Junction Table)
* id
* shirt_id
* material_id
```

#### Junction Tables
We can't efficiently store multiple values in a single field, so M2M fields store all their relationships in a separate table called a "junction table" created just for this purpose. Junction tables are very simple – like all Directus tables they have an `id` column, but they also have two more columns for storing the IDs of the two items it's relating. In this case we're linking a shirts with their respective materials – so we have a `shirt_materials` junction table with `shirt_id` and `material_id` columns.

#### Aliases
Another thing you may have noticed is that the `materials` column says `Alias` and has quotes around it. Since we're not actually storing anything in that column (remember, values are stored in the Junction Table) we don't need to create it in the database. Instead, Directus uses an Alias column (like a ghost column) to represent a column for M2M UIs. Aliases columns don't exist in your database schema, they are added directly into the `directus_columns` table (a good place to look for bulk creation or troubleshooting).

Since relational UIs can get slightly complex, if you can't get one working or run into issues check out our Troubleshooting Relationships section.

----------

### Single File (M2O)
*Supported Datatypes: **`INT`***

This is a M2O relational UI that links a single file (and YouTube/Vimeo video embeds) by storing the related item's ID – which is why this UI only works with the INT datatype (also used for IDs). If you have a `books` table you could use this for the `cover_image` column, for a `projects` table this would be the UI used for columns like: `thumbnail_image`, `wireframe_pdf`, and `background_video`. Basically any column that needs to store a single file.

* `allowed_filetypes`: A CSV of file extensions that this UI will accept. For video embeds you can use `vimeo` and `youtube` as the extension.

----------

### Multiple Files (M2M)
*Supported Datatypes: **`MANYTOMANY` (an alias datatype)***

This is a M2M relational UI that links multiple files (and YouTube/Vimeo video embeds). If you have a `album` table you could use this to store mp3s within `tracks`, for a `projects` table this would be the UI used for columns like: `hero_slideshow`, `youtube_playlist`, and `press_pdfs`. Basically any column that needs to store multiple files.

* `add_button`: Toggles an "Add" button for adding new files directly into the UI
* `choose_button`: Toggles a "Choose" button that opens a modal with all existing Directus files to choose from
* `remove_button`: Toggles "Remove" buttons for each file that let's you delete it

----------

### Many-to-Many (M2M)
*Supported Datatypes: **`MANYTOMANY` (an alias datatype)***

This is a M2M relational UI that will make it easy to link the item being edited to multiple other items from another table (or the same table). You can use this to relate multiple `tags` to `projects`, or multiple `staff` to their respective `office`. But be careful about creating a schema/architecture with recursive or deeply nested M2Ms – otherwise you'll end up with a confusing "Matryoshka doll" user experience.

* `visible_columns`: A column name (or CSV of column names) to show within the interface
* `add_button`: Toggles an "Add" button for adding new items directly into the UI
* `choose_button`: Toggles a "Choose" button that opens a modal with existing table items to choose from
* `remove_button`: Toggles "Remove" buttons for each item that let's you delete it
* `filter_type`: You have two options for how to filter this relational column from the Item Listing page depending on the size of your dataset:
	* Dropdown: For small datasets, this gives a dropdown for easy filtering
	* Text Input: For larger datasets, this open field let's you filter by typing
* `filter_column`: The column who's value is used for filtering
* `visible_column_template`: Handlebars template notation for the fields to show in results. Eg: `{{first_name}} {{last_name}}`. All columns used here must be added to `visible_columns`
* `min_entries`: Sets a minimum number of items that need to be added for this field to validate
* `no_duplicates`: If enabled, items already linked will not show up in the Choose Item listing modal

----------

### Many-to-One (M2O)
*Supported Datatypes: **`INT`***

This is a M2O relational UI drop-down that links to a single item by storing the related item's ID in the column – which is why this UI only works with the INT datatype (also used for IDs). You could use this to relate each item in your `press` table to a `project`, or to relate

* `readonly`: Disables editing of the field while still letting users see the value
* `visible_column`: A column name (or CSV of column names) to show within the interface
	* **TODO: update name to plural, this accepts CSV columns**
* `visible_column_template`: Handlebars template notation for the fields to show in results. Eg: `{{first_name}} {{last_name}}`. All columns used here must be added to `visible_columns`
* `visible_status_ids`: The values of the status column that will be shown/allowed in this UI. If the related table has a status column the default values are: `0 = deleted`, `1 = active`, `2 = draft`
* `placeholder_text`: Grayed out default placeholder text in the input when it's empty
* `filter_type`: You have two options for how to filter this relational column from the Item Listing page depending on the size of your dataset:
	* Dropdown: For small datasets, this gives a dropdown for easy filtering
	* Text Input: For larger datasets, this open field let's you filter by typing
* `filter_column`: The column who's value is used for filtering

----------

### Many-to-One Type-Ahead
*Supported Datatypes: **`INT`***

Similar to the `Many-to-One` in function, the interface for this UI is a type-ahead (live search auto-complete) which is useful for large relational datasets that won't fit into a dropdown.

* `visible_column`: The column name used to search and show for items
* `size`: Adjusts the max width of the input (Small, Medium, Large)
* `template`: Handlebars template for displaying the items
* `include_inactive`: Whether or not to include inactive (`2`) status items

----------

### One-to-Many (O2M)
*Supported Datatypes: **`ONETOMANY` (an alias datatype)***

Similar to Many-to-One, this UI is an interface for the opposite direction. Instead of saving the `id` of a related item in an actual column, the One-to-Many is an Alias column that performs actions on related items.

* `visible_columns`: Which columns to show for related items
* `result_limit`: A maximum number of results to be returned before truncating results
* `add_button`: Toggles an "Add" button for adding new items directly into the UI
* `remove_button`: Toggles "Remove" buttons for each item that let's you delete it