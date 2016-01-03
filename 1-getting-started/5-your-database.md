# Your Database

### Choosing an Existing Schema
If you're looking to get up and running as quickly or possible, you may want to choose from our small but growing [library of schema boilerplates](#). Directus will also work with most SQL schemas you find elsewhere – though the formatting of some table/field names may be less intuitive to users.


### Creating & Customizing Schemas
Whether you're adapting a preexisting database or starting from scratch – the following guidelines will help you get the most out of Directus. Below is an example SQL query for generating a simple table that considers these guidelines:

```
CREATE TABLE `articles` (
  `id` int(11) unsigned NOT NULL AUTO_INCREMENT,
  `active` tinyint(1) unsigned DEFAULT '2',
  `sort` int(11) DEFAULT NULL,
  `title` varchar(100) DEFAULT NULL,
  `article` text,
  `publish_date` datetime DEFAULT NULL,
  `author` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

### Table & Field Naming
Directus auto-formats all table and field names for presentation to the users, so it's important to consider your naming system. Beyond that – you should make sure that your field names would make sense when formatted and read by users.

* Underscores become spaces
* Each word is capitalized
  * Edge-cases are handled by an editable array of overrides
* `_id` is removed from the end of titles
* Tables prepended with `directus_` are hiden within Directus

*Great:*
* `publish_date` becomes `Publish Date`
* `employee_number` becomes `Employee Number`
* `faq_and_support` becomes `FAQ and Support`

*Not so great:*
* `pubDate` becomes `Pubdate`
* `EmpNo` becomes `Empno`
* `FaqSupport` becomes `Faqsupport`

### Primary Key
Currently Directus requires that every table contains an auto-incremented primary key named `id`.
```
`id` int(11) unsigned NOT NULL AUTO_INCREMENT
```

> The abstracting/decoupling of this field name is under development.

### Status Field
If you would like the items of a table to track a "status" state, you can easily do that within Directus. A status could be used in many different ways, but the most common is: *Published*, *Draft*, or *Deleted*, but you could extend or customize this as needed.

It is important when setting up an app to honor any Status states used by Directus. Typically this means only showing active/published content. Assuming you are using the default Status options, that would mean limiting all SQL queries to:
```
AND `active` = '1'
```

[Learn More](https://github.com/directus/docs/blob/master/3-developer/2-configuration.md)

### Sort Field
Adding a `sort(INT11)` field to a table turns on Directus' drag-and-drop sorting. Items on the Directus listing page will now have handles for dragging them into curated orders. When sorted, Directus will save ascending integers into the order field, thereby making it easy to return results in this order:

```
ORDER BY `sort` ASC
```

> If a table will likely have many items (), it may be advisable not to use the manual sort feature. Dragging items within long lists can be difficult – and the sort feature disables when items span multiple pages.

### Datatypes
Directus uses the datatype of the field to determine which Inputs/Interfaces are allowed. The most common one is chosen as a default, but you can always change this in the *Settings > Tables & Inputs*. Below are a few examples of how a datatype may be used:

* VARCHAR(200) – By default this would be a regular text field with a input countdown of remaining characters, but you could change it to a select dropdown of options.
* TINYINT(1) – By default this would be a checkbox (`0` or `1`), but you could change it to a single number input.
* TEXT – By default this is a simple text area, but you could change it to a WYSIWYG editor.
* DATETIME – By default this will show an HTML5 date and time inputs, but you could change it to track the last Directus user to save this item.

### Defaults
Directus uses your database defaults for all inputs/interfaces. So if you give that `TINYINT` a default value of `1`, the checkbox input will be checked by default.

### Comments
You can add field comments directly in your database, those will auto matically get pulled in to the user as a note on that input. This is especailly useful to help clarify field names and purpose for the users of Directus.

### Relationships
If you're looking to create relationships in your database this is done through relational ids (one-to-many) and junction-tables (many-to-many). Since Directus requires an `id` unique primary key for each table, this is what is saved in the INT(11) relational field you setup.

#### One-to-Many & Many-to-One
The easiest relationships, these are created within Directus or the database itself. In the example below, we're 

1. Create the field to store the related table's id
2. Setup the relationship within Directus or using the following query:

```SQL
INSERT INTO `directus_columns`
  (`table_name`, `column_name`, `data_type`, `ui`, `relationship_type`, `table_related`, `junction_key_right`)
VALUES
  ('articles', 'author', 'INT', 'many_to_one', 'MANYTOONE', 'directus_users', 'user');
```

#### Many-to-Many
Again, these can be created within Directus or the database itself. In the example below, to create a slideshow interface we're adding in a relationship between the `articles` table we just created and the `directus_files` table.

##### Create the junction table
Remember to add the id column and two fields for holding the relational id.

> Optional Note: You can add a `sort` column (see above) to allow the relational items to be manually sorted with drag-and-drop.

```SQL
CREATE TABLE `article_images` (
  `id` int(11) unsigned NOT NULL AUTO_INCREMENT,
  `sort` int(11) DEFAULT NULL,
  `article_id` int(11) DEFAULT NULL,
  `file_id` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

##### Setup the relationship
Can be done within Directus or using the following query:

```SQL
INSERT INTO `directus_columns`
  (`table_name`, `column_name`, `data_type`, `ui`, `relationship_type`, `table_related`, `junction_table`, `junction_key_left`, `junction_key_right`)
VALUES
  ('articles', 'slideshow', 'MANYTOMANY', 'multiple_files', 'MANYTOMANY', 'directus_files', 'article_images', 'article_id', 'file_id')
```

### Field Order
By default Directus will display table inputs in the same order as the database fields, however this can be overridden within *Directus Settings>Tables & Inputs*. The reason we don't alter the fields within the database itself when changing input order is because some database optimization involves the specific ordering of the fields.

