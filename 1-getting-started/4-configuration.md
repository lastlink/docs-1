# Configuration
Now that you have Directus installed, you can customize it for your specific project. The first Directus user is always an administrator, which gives you access to the Directus Settings by clicking on the gear at the bottom of the sidebar. 

------

### Global Settings
Personalize this instance of Directus to fit your organization’s needs. Change colors, add a company logo, set the auto logout time, etc

* **Site Name:** The name of your project that appears in the browser title
* **Site URL:** Clicking the main logo takes you to this URL
* **CMS User Auto Sign Out:** The number of minutes before users are automatically logged out of Directus
* **Rows Per Page:** The number of items shown on each item listing page
* **CMS Thumbnail URL:** Directus is minimally stylized and unbranded so it can be easily tailored to match your brand/project. Enter the URL to your **170×100px** logo image here – use a PNG with alpha-transparency for a more polished look.*

------

### File & Thumbnail Settings
Here you can adjust the size and quality of your automatic thumbnails, decide where to save uploaded files, and much more.

* **File Naming:** This determines the naming convention for files uploaded through Directus.
    * *File Name*: Saves files using a cleaned-up version of the original file name. Duplicate file names are appended with an integer so no files are accidentally overwritten.
    * *File ID* (default): Saves files with the database ID padded with leading zeros to a length of 11.
    * *File Hash*: A unique hash of the file/upload datetime. This option is ideal when file URLs should not be predictable.
* **Thumbnail Quality:** (0-100, 100 is default) – This is the jpg quality thumbnails within Directus. This value does not influence the actual files you upload through Directus, only the system's thumbnail.
* **Thumbnail Crop Enabled:** When checked (default), Directus will generate system thumbnails for images as a square – other aspect ratios will be cropped to a square. If unchecked, Directus will generate scaled down system thumbnails that maintain their orignal aspect ratio (uncropped).

> Changing these values will **not** effect any files already uploaded into Directus.

------

### Tables & Inputs
Here you can create new tables and fields, or if managing an existing database, Directus provides intelligent default interfaces based on your datatypes. Either way, the real power comes from being able to make broad and granular adjustments to how Directus handles your inputs, interfaces, validation, and visualizations.

#### Table Options
* **Hidden:** Determines if the table is hidden (not restricted) from all users. This affects the sidebar navigation and table-listing page.
* **Single:** While not a traditional way to architect a database, sometimes you may find yourself with a table intended to contain only a single item/record. Perhaps you want to manage the content on a website's "About" page with the fields: `title`, `hero_image`, and `company_description`. Any table marked as "single" will skip the _Item Listing_ page and take users directly to the _Edit Item_ page. Note: The item/record should have an ID of `1`.
* **Is Junction Table:** Junction tables (aka: *cross-reference table, bridge table, join table, map table, intersection table*) connect items within different tables through "many-to-many" relationships. Junction tables store relationships created by User Interfaces (UIs) and are not editable directly within Directus.

#### Field Options
Clicking a table within _Settings > Tables & Inputs_ lets you customize its individual fields. System fields such as `id`, `active`, and `sort` are displayed grayed out at the top.

* **Reordering Fields** Using the handle on the far left of each column you can adjust the presented order of fields on the _Edit Item_ page.
* **Field** This is the column name, hover over this text to see its database datatype/length. Column names run through a Directus prettify function to be more presentable system-wide; underscores become spaces, words become Title Case, and certain letter-pairings are given special capitalization (such as "pH" or "URL"). Relational fields have an indicator to the right showing the relationship type ("⊢" for many-to-one, "⊢⊣" for many-to-many).
* **Input Type** Here you can change the default User-Interface (UI) for each field, choosing between options that support the field's datatype (eg: varchar, tinyint).
    * Example: You have an `INT` column named `hero_image` – by default Directus would show this as a numeric-only text input. By changing the _Input Type_ from "Numeric" to "Single File" this field now shows a file upload interface, storing the relational file ID as its value. For more information on Directus' Core UIs, [click here](https://github.com/RNGR/directus6/wiki/4.-Extending-Directus#custom-inputs-uis).
* **Input Type Options (gear icon)** Clicking the gear opens an overlay containing all options for the selected _Input Type_. For example, the "WYSIWYG Editor" has options including which formatting buttons are displayed (eg: limiting to *bold* and *italics*)
* **Relationship Settings (flow-tree icon)** Relational fields will have this additional icon allowing you to manage settings. _Note: At this time, developers may find it easier to manage these settings directly within the database table `directus_columns`._
   * _Data Type_: ManyToOne or ManyToMany
   * _Related Table_: The name of the related table
* **Hidden** Used for globally hiding this field from listing and edit pages for all groups.
* **Required** If selected, this field name will display an asterisk and be required to save the item.
    * Note: UIs may handle being required in unexpected ways – imagine a required checkbox or slider interface. Ultimately, this option only turns on the "validate" function within the UI code – which may not be enforced by some _custom_ UIs.
* **Primary** This radio button denotes which field within this table best represents it uniquely. It is used on pages like activity, where items need to be referred to contextually. _Note: This is **not** the table's primary-key._
* **Note** Use this to add additional field info or notes on the item edit page. Since Directus uses field names as input labels this can help add clarity for field use. It can help guide formatting or remind users of required pixel dimensions for image inputs. _Note: While notes allow for the use of HTML, please use caution and discretion._

#### Creating New Tables

1. Navigate to the _Settings > Tables & Inputs_
    * Access _Settings_ from the gear at the bottom of the sidebar
2. Click the (+) button at the top of the page
3. Type the name of the table and hit OK
4. Click on the table within the listing to add fields

> You can always add Tables directly to your database – then follow the steps below to allow that table to be managed by Directus.

#### Creating New Fields

1. Navigate to the _Settings > Tables & Inputs_
    * Access _Settings_ from the gear at the bottom of the sidebar
2. Click on the table name you want to add the field to
3. Click the "Add New Field: button at the bottom of the page
4. Choose a field name and UI Type and click save
    * Optionally, you can update the Data Type or Length

> You can always add new Fields directly to your database – then refresh Directus and they will apear.

------

### Users, and Group Permissions
Chances are that additional users will need to access Directus. You can add as many users as you want within Directus, each assigned to a user-group with specific access/permissions.

#### Creating New User-Groups
1. Navigate to the _Settings > Group Permissions_
    * Access _Settings_ from the gear at the bottom of the sidebar
2. Click the (+) button at the top of the page
2. Type the name of the group and hit OK
3. Click on the group within the listing to set its specific permissions.

#### Creating New Users
1. Navigate to the _Users_ page from the sidebar
2. Click the (+) button at the top of the page
3. Fill in the applicable fields. Required fields include:
    * First Name
    * Last Name
    * Email
    * Password
    * Group
4. Save the user
