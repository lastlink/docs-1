#Inputs & Interfaces

User Interfaces (UIs) are how your users will interact with the different types of content in your database. Each field in your database has a data-type that determines what kind of content can be stored there – Directus uses this information to determine a default UI and any other UIs that are supported. In addition to the provided Core UIs, you can also easy create new Custom UIs for specific or complex use-cases.

### Text & Character Inputs
#### Text Input
*Supported Datatypes: **`VARCHAR`**, `DATE`, `TIME`, `ENUM`*

A simple, basic, single-line text field for almost any kind of string data. The user is shown the remaining character count based on the length property of the column. Despite being so simple, a few key options make this UI one of the most useful and flexible:

* `readonly`: Disables editing of the field while still letting users see the value
* `size`: Adjusts the max width of the input (Small, Medium, Large)
* `placeholder_text`: Grayed out default placeholder text in the input when it's empty
* `validation_type`: Chooses the type of validation used on this field
	* Character Blacklist: Choose the specific characters **not** allowed in the input
	* Character Whitelist: Choose the specific characters allowed in the input
	* RegEx: Create a regular expression to validate the value. Useful for emails, phone number formatting, or almost anything
* `validation_string`: Holds the CSV list of Whitelist/Blacklist characters or the RegEx value (based on the above option)
* `validation_message`: A message that is shown to the user if the validation fails

#### Text Area
*Supported Datatypes: **`TEXT`**, `VARCHAR`*

A multi-line text field for longer plain-text data. New lines are saved in the database as new lines as this input does not create any HTML tags.

* `rows`: The number of text rows available for the input before scrolling

#### WYSIWYG
*Supported Datatypes: **`VARCHAR`**, `TEXT`*

A multi-line text field for longer HTML content with WYSIWYG formatting buttons. Each formatting button can be toggled on or off as needed.

* `readonly`: Disables editing of the field while still letting users see the value
* `height`: The input's height in pixels before scrolling. Default: 500px
* `available format buttons`: `bold`, `italic`, `underline`, `strikethrough`, `rule`, `create_link`, `insert_image`, `embed_video`, `embed_width`, `embed_height`, `html`, `ordered_list`, `h1`, `h2`, `h3`, `h4`, `h5`, `h6`, `blockquote`, `ul`, `ol`

#### Slug, or Short Name
*Supported Datatypes: **`VARCHAR`***

Often clean/semantic URLs will include a contextual identifier based on an item's title rather than the `id` alone. This UI automatically creates that URL-friendly value based on another input. For instance, if linked to the `title` column, as the user types "This, That & the Other!" the `slug` input would live-update to "this-that-the-other".

* `readonly`: Disables editing of the field while still letting users see the value
* `size`: Adjusts the max width of the input (Small, Medium, Large)
* `mirrored_field`: Enter the column name of the field the slug will pull it's value from

#### Password & Salt
*Supported Datatypes: **`VARCHAR`***

This UI contains a masked input for entering a password, a second input to confirm the password, a "Generate New" button for optionally generating new secure passwords quickly, and a "Reveal Password" toggle to expose the password to the user in plain-text. This UI can also be linked to a "salt" column so that the password entered is securely hashed.

* `require_confirmation`: Toggles the second input ("Confirm Password"). On by default.
* `salt_field`: The name of the column to be used as a salt in the password hash. Default: `salt`

#### Numeric
*Supported Datatypes: **`TINYINT`**, `INT`, `NUMERIC`, `FLOAT`, `YEAR`, `VARCHAR`, `CHAR`, `DOUBLE`, `BIGINT`*

**TODO: Combine with `text-field`**. A simple input that only accepts number characters. Alternatively you could use the `text-input` UI and set the appropriate validation.

* `size`: Adjusts the max width of the input (Small, Medium, Large)
* `allow_null`: Whether the input will allow for `NULL` values (empty input). If disabled then an empty input is converted to `0`.

#### Color
*Supported Datatypes: **`VARCHAR`***

Accepts only 6 hexadecimal characters and provides a live-colored square matching the value. This UI also uses the HTML5 color-chooser for easy color selection. Allowed hexadecimal characters include: `0123456789ABCDEF`

* `readonly`: Disables editing of the field while still letting users see the value
* `show_color_on_list`: Shows a color box representation on the Item Listing page

----------

### Date & Time Inputs
**TODO – All these UIs should be combined into one**

#### Datetime (Date, Time, and Year)
*Supported Datatypes: **`DATETIME`**, `DATE`, `TIME`, `YEAR`*
This UI provides a set of drop-downs and numerical inputs for entering months days, years, hours, minutes and seconds based on the datatype. HTML5 helpers are available for easier date/time selection. All values are saved in the ISO 8601 standard: yyyy-mm-dd hh-mm-ss

* `readonly`: Disables editing of the field while still letting users see the value
* `format`: The display format for the date/time on the Item Listing page. This does not influence how data is saved.
* `include_seconds`: A boolean for whether to show seconds or not. Sometimes you don't need that level of accuracy and want to keep the interface as simple as possible.
* `contextual_date_in_listview`: Will show the date/time on the Item Listing page as a time-ago. For example: `just now`, `30s ago`, `2h ago`, or `3w ago`

----------

### Relational Data

Since SQL is a relational database, Directus has several UIs that can help clearly and easily manage relationships between items. An item can have related items from the same table (eg: *Project -> Related Project*) or a different table (eg: *Project -> Category*). An item can also have relationships to a single item (eg: *Shirt -> Size*) in a Many-to-One (or One-to-Many) relationship, or to multiple items (eg *Shirt -> Materials*) through Many-to-Many relationships.

**Many-to-One** (M2O) relationships save the `id` from another item as it's value, creating a dynamic relationship to that item. 

**Many-to-Many** (M2M) relationships are quite a bit more complex, but very powerful. There are two things that are important to understand for M2Ms: Junction Tables, and Aliases. Let's use our *Shirt -> Materials* example from before to explore how this works:

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

**Junction Tables**
We can't efficiently store multiple values in a single field, so M2M fields store all their relationships in a separate table called a "junction table" created just for this purpose. Junction tables are very simple – like all Directus tables they have an `id` column, but they also have two more columns for storing the IDs of the two items it's relating. In this case we're linking a shirts with their respective materials – so we have a `shirt_materials` junction table with `shirt_id` and `material_id` columns.

**Aliases**
Another thing you may have noticed is that the `materials` column says `Alias` and has quotes around it. Since we're not actually storing anything in that column (remember, values are stored in the Junction Table) we don't need to create it in the database. Instead, Directus uses an Alias column (like a ghost column) to represent a column for M2M UIs. Aliases columns don't exist in your database schema, they are added directly into the `directus_columns` table (a good place to look for bulk creation or troubleshooting).

Since relational UIs can get slightly complex, if you can't get one working or run into issues check out our Troubleshooting Relationships section.

#### Single File (M2O)
*Supported Datatypes: **`INT`***

This is a M2O relational UI that links a single file (and YouTube/Vimeo video embeds) by storing the related item's ID – which is why this UI only works with the INT datatype (also used for IDs). If you have a `books` table you could use this for the `cover_image` column, for a `projects` table this would be the UI used for columns like: `thumbnail_image`, `wireframe_pdf`, and `background_video`. Basically any column that needs to store a single file.

* `allowed_filetypes`: A CSV of file extensions that this UI will accept. For video embeds you can use `vimeo` and `youtube` as the extension.

#### Multiple Files (M2M)
*Supported Datatypes: **`MANYTOMANY` (an alias datatype)***

This is a M2M relational UI that links multiple files (and YouTube/Vimeo video embeds). If you have a `album` table you could use this to store mp3s within `tracks`, for a `projects` table this would be the UI used for columns like: `hero_slideshow`, `youtube_playlist`, and `press_pdfs`. Basically any column that needs to store multiple files.

* `add_button`: Toggles an "Add" button for adding new files directly into the UI
* `choose_button`: Toggles a "Choose" button that opens a modal with all existing Directus files to choose from
* `remove_button`: Toggles "Remove" buttons for each file that let's you delete it

#### Many-to-Many (M2M)
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

#### Many-to-One (M2O)
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

#### Many-to-One Type-Ahead
*Supported Datatypes: **`INT`***

Similar to the `Many-to-One` in function, the interface for this UI is a type-ahead (live search auto-complete) which is useful for large relational datasets that won't fit into a dropdown.

* `visible_column`: The column name to show for items
* `size`: Adjusts the max width of the input (Small, Medium, Large)
* `template`: Handlebars template for displaying the items
* `include_inactive`: Whether or not to include inactive (`2`) status items

#### One-to-Many (O2M)
*Supported Datatypes: **`ONETOMANY` (an alias datatype)***

Similar to Many-to-One, this UI is an interface for the opposite direction. Instead of saving the `id` of a related item in an actual column, the One-to-Many is an Alias column that performs actions on related items.

* `visible_columns`: Which columns to show for related items
* `result_limit`: A maximum number of results to be returned before truncating results
* `add_button`: Toggles an "Add" button for adding new items directly into the UI
* `remove_button`: Toggles "Remove" buttons for each item that let's you delete it

----------

### Lists and Other Inputs

#### Select (Drop-down or Radio Buttons)
*Supported Datatypes: **`VARCHAR`**, `INT`*

Sometimes you don't need to create a dedicated table to house relational dropdown options but you still want to limit the values a user can choose. This UI will save a single non-relational value chosen from a set of JSON options.

**TODO: Merge in `Radio Buttons`** 

* `options`: JSON key-value-pairs where the key is what's saved to the database, and the value is what's shown in the dropdown interface
* `allow_null`: Whether the input will allow for `NULL` values (empty input). If disabled then an empty input is converted to `0`
* `placeholder_text`: The text for the first/empty dropdown option

#### Multi-Select (List or Checkboxes)
*Supported Datatypes: **`VARCHAR`**, `TEXT`*

Sometimes you don't need to create a dedicated table to house relational dropdown options but you still want to limit the values a user can choose. This UI will save multiple non-relational values from a set of JSON options. All selections are glued together with a delimiting character.

* `type`: The way that the data will be visualized, there are two options:
	* Select List: A box with options that accept multiple selections. This box scrolls, but it not good for very large datasets
	* Checkbox List: A set of checkboxes that can be individually turned on/off. The advantage here is that all can be seen at once
* `delimiter`: The character that will be used as the glue when "imploding" or combining the values selected in the UI. Typically a comma is used such as in a CSV
* `options`: JSON key-value-pairs where the key is what's saved to the database, and the value is what's shown in the dropdown interface

    For the list view users select multiple items using the control/ctrl key (Windows) or command/cmd key (Mac).

#### Tags
*Supported Datatypes: **`TEXT`**, `VARCHAR`, `CHAR`*

A system for entering and saving comma-delimited tags – for relational tags use the `many-to-many` UI instead. Tags are entered into the list upon hitting the comma or enter key and are deleted by clicking the tag in the list. The tags are saved into the database as a CSV string with commas at the beginning and end (",ranger,studio,range,") which lets you perform powerful `LIKE` filters. For example, by using commas you can filter with `%,range,%` to get results that are exact (does not include "ranger") or `%range%` for inclusive (does include "ranger"). 

* `force_lowercase`: When on, all entered tags are converted to lowercase

#### Checkbox
*Supported Datatypes: **`TINYINT`***

Checkbox is the default UI for the TINYINT datatype – saving either a `1` (checked) or `0` (unchecked). It also honors the default value of the database, which is the proper way to set the UI's initial state.

#### Slider
*Supported Datatypes: **`INT`***

An HTML5 adjustable slider for choosing a number.

* `minimum`: The minimum numeric value
* `maximum`: The maximum numeric value
* `step`: This sets the interval for allowed values

#### Instructions
*Supported Datatypes: **`VARCHAR`**, `TEXT`*

**TODO: Add `ALIAS` datatype support and remove `VARCHAR` and `TEXT`. No need to have an actual column for this.**

This is an easy way to include verbose or formatted instructions or other helper information within the Item Detail page. If the column Note isn't enough room to adequately describe the column's guidelines or you need table/level instructions, this is a good way to add context.

* `instructions`: This WYSIWYG editor allows you to add formatted text, images, or any other content that will help guide CMS users through the details of your content workflow.

#### Map
*Supported Datatypes: **`VARCHAR`**, `ALIAS`*

This UI provides an visual and interactive way to select a specific location, which is then Geocoded and dynamically fills in any linked address fields.

* `apiKey`: Google API Key (Provided by Google). Required due to API limitations
* `street_number_field`: Column name that will accept the street number when a location is chosen
* `street_field`: Column name that will accept the street name when a location is chosen
* `city_field`: Column name that will accept the city when a location is chosen
* `postal_code_field`: Column name that will accept the postal code (zip) when a location is chosen
* `state_field`: Column name that will accept the state name when a location is chosen
* `stateCode_field`: Column name that will accept the state code (eg: NY) when a location is chosen
* `country_field`: Column name that will accept the country when a location is chosen
* `countryCode_field`: Column name that will accept the country code (US) when a location is chosen
* `mapHeight`: The height of the map in pixels. Default is 400px
* `showLatLng`: 

----------

### System Inputs
*These are Core UIs that are used exclusively by the Directus framework for internal purposes.*

* directus_activity
* directus_columns
* directus_file
* directus_file_size
* directus_file_title
* directus_messages_recipients
* directus_user
* directus_user_activity
* directus_user_avatar

----------

### Other UIs to Document
* blob
* enum
* random
* system – **TODO: Rename to `status`**
* template_chooser
* translation
* user

----------

### Custom Inputs & Interfaces
Use the following steps to create your own custom user interfaces using the above as starter templates.

1. Copy a Core UI file from `/app/core-ui` into the custom UI directory: `/ui`
2. Set a unique name for the UI: `Module.id`
3. Choose which SQL datatypes this UI will support: `Module.dataTypes`
4. Optionally, add UI Options that admin users can adjust per column: `Module.variables`
5. Draft up some markup with inline styling within the `template` variable.
	* You will also see examples of escaped CSS in the template variable, but remember to namespace any styling.
6. Add any validation into the `Module.validate` function which is called when attempting to save the model. If there is an error message the system automatically shows it as an alert. There are two parameters available within this function:
	* **value**: String : Submitted value for this column's UI
	* **options**: Object : Contains the options from `Module.variables` for this UI
		* collection [TableCollection]
		* model [EntriesModel]
		* schema
		* settings
7. Finally, format the value for display on the Item Listing page within the `Module.list` function. There is one parameter available:
	* **options**: Object : Contains the value and options for this UI
		* value
		* collection [TableCollection]
		* model [EntriesModel]
		* schema
		* settings


At this point, all you have to do is refresh your instance of Directus and your new UI will be available. If you go to `Settings > Tables & Inputs > []Table]` and open the User Interface dropdown for the desired column, if that column's datatype is supported you will see your UI as an option. If you don't see it, confirm that that datatype is listed in `Module.dataTypes` and that the `Module.id` is unique – otherwise check the error logs.