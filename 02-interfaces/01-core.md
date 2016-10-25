# Core Interfaces

User Interfaces (UIs) are how your users will interact with the different types of content in your database. Each field in your database has a data-type that determines what kind of content can be stored there – Directus uses this information to determine a default UI and any other UIs that are supported. In addition to the provided Core UIs, you can also easy create new Custom UIs for specific or complex use-cases.

----------

### Text Input
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

----------

### Text Area
*Supported Datatypes: **`TEXT`**, `VARCHAR`*

A multi-line text field for longer plain-text data. New lines are saved in the database as new lines as this input does not create any HTML tags.

* `rows`: The number of text rows available for the input before scrolling

----------

### WYSIWYG
*Supported Datatypes: **`VARCHAR`**, `TEXT`*

A multi-line text field for longer HTML content with WYSIWYG formatting buttons. Each formatting button can be toggled on or off as needed.

* `readonly`: Disables editing of the field while still letting users see the value
* `height`: The input's height in pixels before scrolling. Default: 500px
* `available format buttons`: `bold`, `italic`, `underline`, `strikethrough`, `rule`, `create_link`, `insert_image`, `embed_video`, `embed_width`, `embed_height`, `html`, `ordered_list`, `h1`, `h2`, `h3`, `h4`, `h5`, `h6`, `blockquote`, `ul`, `ol`

----------

### Slug, or Short Name
*Supported Datatypes: **`VARCHAR`***

Often clean/semantic URLs will include a contextual identifier based on an item's title rather than the `id` alone. This UI automatically creates that URL-friendly value based on another input. For instance, if linked to the `title` column, as the user types "This, That & the Other!" the `slug` input would live-update to "this-that-the-other".

* `readonly`: Disables editing of the field while still letting users see the value
* `size`: Adjusts the max width of the input (Small, Medium, Large)
* `mirrored_field`: Enter the column name of the field the slug will pull it's value from

----------

### Password & Salt
*Supported Datatypes: **`VARCHAR`***

This UI contains a masked input for entering a password, a second input to confirm the password, a "Generate New" button for optionally generating new secure passwords quickly, and a "Reveal Password" toggle to expose the password to the user in plain-text. This UI can also be linked to a "salt" column so that the password entered is securely hashed.

* `require_confirmation`: Toggles the second input ("Confirm Password"). On by default.
* `salt_field`: The name of the column to be used as a salt in the password hash. Default: `salt`

----------

### Numeric
*Supported Datatypes: **`TINYINT`**, `INT`, `NUMERIC`, `FLOAT`, `YEAR`, `VARCHAR`, `CHAR`, `DOUBLE`, `BIGINT`*

**TODO: Combine with `text-field`**. A simple input that only accepts number characters. Alternatively you could use the `text-input` UI and set the appropriate validation.

* `size`: Adjusts the max width of the input (Small, Medium, Large)
* `allow_null`: Whether the input will allow for `NULL` values (empty input). If disabled then an empty input is converted to `0`.

----------

### Hex Color
*Supported Datatypes: **`VARCHAR`***

Accepts only 6 hexadecimal characters and provides a live-colored square matching the value. This UI also uses the HTML5 color-chooser for easy color selection. Allowed hexadecimal characters include: `0123456789ABCDEF`

* `readonly`: Disables editing of the field while still letting users see the value
* `show_color_on_list`: Shows a color box representation on the Item Listing page

----------

### Datetime (Date, Time, and Year)
*Supported Datatypes: **`DATETIME`**, `DATE`, `TIME`, `YEAR`*
This UI provides a set of drop-downs and numerical inputs for entering months days, years, hours, minutes and seconds based on the datatype. HTML5 helpers are available for easier date/time selection. All values are saved in the ISO 8601 standard: yyyy-mm-dd hh-mm-ss

* `readonly`: Disables editing of the field while still letting users see the value
* `format`: The display format for the date/time on the Item Listing page. This does not influence how data is saved.
* `include_seconds`: A boolean for whether to show seconds or not. Sometimes you don't need that level of accuracy and want to keep the interface as simple as possible.
* `contextual_date_in_listview`: Will show the date/time on the Item Listing page as a time-ago. For example: `just now`, `30s ago`, `2h ago`, or `3w ago`

----------

### Select (Drop-down or Radio Buttons)
*Supported Datatypes: **`VARCHAR`**, `INT`*

Sometimes you don't need to create a dedicated table to house relational dropdown options but you still want to limit the values a user can choose. This UI will save a single non-relational value chosen from a set of JSON options.

**TODO: Merge in `Radio Buttons`** 

* `options`: JSON key-value-pairs where the key is what's saved to the database, and the value is what's shown in the dropdown interface
* `allow_null`: Whether the input will allow for `NULL` values (empty input). If disabled then an empty input is converted to `0`
* `placeholder_text`: The text for the first/empty dropdown option

----------

### Multi-Select (List or Checkboxes)
*Supported Datatypes: **`VARCHAR`**, `TEXT`*

Sometimes you don't need to create a dedicated table to house relational dropdown options but you still want to limit the values a user can choose. This UI will save multiple non-relational values from a set of JSON options. All selections are glued together with a delimiting character.

* `type`: The way that the data will be visualized, there are two options:
	* Select List: A box with options that accept multiple selections. This box scrolls, but it not good for very large datasets
	* Checkbox List: A set of checkboxes that can be individually turned on/off. The advantage here is that all can be seen at once
* `delimiter`: The character that will be used as the glue when "imploding" or combining the values selected in the UI. Typically a comma is used such as in a CSV
* `options`: JSON key-value-pairs where the key is what's saved to the database, and the value is what's shown in the dropdown interface

    For the list view users select multiple items using the control/ctrl key (Windows) or command/cmd key (Mac).

----------

### Tags
*Supported Datatypes: **`TEXT`**, `VARCHAR`, `CHAR`*

A system for entering and saving comma-delimited tags – for relational tags use the `many-to-many` UI instead. Tags are entered into the list upon hitting the comma or enter key and are deleted by clicking the tag in the list. The tags are saved into the database as a CSV string with commas at the beginning and end (",ranger,studio,range,") which lets you perform powerful `LIKE` filters. For example, by using commas you can filter with `%,range,%` to get results that are exact (does not include "ranger") or `%range%` for inclusive (does include "ranger"). 

* `force_lowercase`: When on, all entered tags are converted to lowercase

----------

### Checkbox
*Supported Datatypes: **`TINYINT`***

Checkbox is the default UI for the TINYINT datatype – saving either a `1` (checked) or `0` (unchecked). It also honors the default value of the database, which is the proper way to set the UI's initial state.

----------

### Slider
*Supported Datatypes: **`INT`***

An HTML5 adjustable slider for choosing a number.

* `minimum`: The minimum numeric value
* `maximum`: The maximum numeric value
* `step`: This sets the interval for allowed values

----------

### Instructions
*Supported Datatypes: **`VARCHAR`**, `TEXT`*

**TODO: Add `ALIAS` datatype support and remove `VARCHAR` and `TEXT`. No need to have an actual column for this.**

This is an easy way to include verbose or formatted instructions or other helper information within the Item Detail page. If the column Note isn't enough room to adequately describe the column's guidelines or you need table/level instructions, this is a good way to add context.

* `instructions`: This WYSIWYG editor allows you to add formatted text, images, or any other content that will help guide CMS users through the details of your content workflow.

----------

### Map
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