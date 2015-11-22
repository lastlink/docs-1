# Configuration
Now that you have Directus installed, you can customize it for your specific project. The first Directus user is always an administrator, which gives you access to the Settings gear at the bottom of the sidebar. There are four sections within Settings:

## Global Settings
* **Site Name:** The name of your project that appears in the browser title
* **Site URL:** Clicking the main logo takes you to this URL
* **CMS User Auto Sign Out:** The number of minutes before users are automatically logged out of Directus
* **Rows Per Page:** The number of items shown on each item listing page
* **CMS Thumbnail URL:** Directus is minimally stylized and unbranded so it can be easily tailored to match your brand/project. Enter the URL to your **170×100px** logo image here – use a PNG with alpha-transparency for a more polished look.*

## Files & Thumbnail Settings
_Note: Changing these values will **not** effect any files already uploaded into Directus._
* **File Naming:** This determines the naming convention for files uploaded through Directus.
    * *File Name*: Saves files using a cleaned-up version of the original file name. Duplicate file names are appended with an integer so no files are accidentally overwritten.
    * *File ID* (default): Saves files with the database ID padded with leading zeros to a length of 11.
    * *File Hash*: A unique hash of the file/upload datetime. This option is ideal when file URLs should not be predictable.
* **Thumbnail Quality:** (0-100, 100 is default) – This is the jpg quality thumbnails within Directus. This value does not influence the actual files you upload through Directus, only the system's thumbnail.
* **Thumbnail Crop Enabled:** When checked (default), Directus will generate system thumbnails for images as a square – other aspect ratios will be cropped to a square. If unchecked, Directus will generate scaled down system thumbnails that maintain their orignal aspect ratio (uncropped).

## Users, Groups, & Permissions
Chances are that additional users will need to access Directus. You can add as many users as you want within Directus, each assigned to a user-group with specific access/permissions.

### Creating New User-Groups
1. Navigate to the _Settings > Group Permissions_
    * Access _Settings_ from the gear at the bottom of the sidebar
2. Click the (+) button at the top of the page
2. Type the name of the group and hit OK
3. Click on the group within the listing to set its specific permissions.

### Creating New Users
1. Navigate to the _Users_ page from the sidebar
2. Click the (+) button at the top of the page
3. Fill in the applicable fields. Required fields include:
    * First Name
    * Last Name
    * Email
    * Password
    * Group
4. Save the user

# Tables & Input Settings

## Table Options
* **Hidden:** Determines if the table is hidden (not restricted) from all users. This affects the sidebar navigation and table-listing page.
* **Single:** While not a traditional way to architect a database, sometimes you may find yourself with a table intended to contain only a single record. Perhaps you want to manage data/fields specific to a single website page such as the homepage. Add any desired fields to a table and mark it as "single" – this will bypass the item listing page when being accessed since there is only one item. (Directus assumes a id of 1)
* **Junction Table:** Mark any junction tables (aka: *cross-reference table, bridge table, join table, map table, intersection table*) as such so that directus is aware.
* **Footer:** Turning on the footer will add useful dynamic info to the bottom of the item listing page tabular data. Including:
    * **SUM** Adds up all column values from each visible item
    * **MIN** Shows the lowest column value within all visible items
    * **MAX** Shows the highest column value within all visible items
    * **AVG** Shows the average of all column values within all visible items

## Field Options
Clicking the table name on **Settings > Tables & Inputs** page will give you additional options at the field level. System fields are displayed grayed out at the top, and lack options.

* **Reordering Fields** Using the handle on the far left of each column you can adjust the presented order of fields on the edit page.
* **Field** This is the column name, hover over the text to see the db data-type. Column names run through a Directus prettify function to be more presentable system-wide; underscores become spaces, words become Title Case, and certain letter-pairings are given special capitalization (such as "pH" or "iOS"). To the right of the text for relational field aliases are indicators of the relationship type (such as "⊢⊣" for many-to-many).
* **Input Type** This is one of the key aspects of Directus – here you can change from the default input UI for each column. Based on the datatype of the column (varchar, tinyint) certain core/custom input interfaces are allowed. For instance, you may have an `INT` column named `hero_image` – by default this Directus input would be a numeric only text input. But the column's "Input Type" dropdown will allow you to make it a file upload interface on the edit page that stores a relational file.id. For more information about creating custom UIs for certain datatypes, [click here](https://github.com/RNGR/directus6/wiki/4.-Extending-Directus#custom-inputs-uis).
* **Input Type Options (gear icon)** Clicking the gear opens an overlay containing all options for the chosen Input Type. For example, if the Input Type is "WYSIWYG Editor" then options include changing which buttons are displayed for this field – so, only *bold* and *italics*, for instance.
* **Hidden** Checking this will globally hide this field from listing and edit pages for all groups.
* **Required** Checking this will enforce the "validate" function within the UI. Required fields will have an asterisk beside them on the item edit page. UIs may treat "required" in different ways... some odd ones include, a required checkbox or slider.
* **Primary** This radio button denotes which field within this table best represents it uniquely. It is used on pages like activity, where items need to be referred to contextually.
* **Note** Use this to add additional field info or notes on the item edit page. Since Directus uses field names as input labels this can help add clarity for field use. It can help guide required pixel dimensions for image inputs, or remind users of formatting. It does allow for the use of HTML – but use that with care.
