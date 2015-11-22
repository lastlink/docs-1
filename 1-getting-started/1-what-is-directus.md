
# What is Directus?
_Directus is a free and open-source SQL database GUI for intuitively managing your project’s content_

### So, is it a CMS or a Database Administration Tool?
As a developer, you're probably already managing content directly through Sequel-Pro, phpMyAdmin, or the command line. These are excellent tools because you get complete control with no setup other than entering the database credentials... but you would never give that access to clients, designers, or inexperienced engineers. Handling relational ids, media/file references, and data validation just isn't intuitive at that level – let alone the risk of accidentally deleting/truncating a table.

Now imagine you could allow anyone to manage that same database content through a simple, intuitive, and feature-rich interface – tailoring table/field access with granular user permissions. Innumerable Content Management Systems are probably coming to mind, but typically those bake-in entire front-end templating solutions, require complicated proprietary database schemas, and generally make a lot of assumptions about what you're doing and how to do it. Maybe the database isn't even _for_ a website – maybe it's for a native app, an inventory system, or internal project management. 

_Below is a comparison of data/content management options_

Feature                                       | Directus Framework    |  Database Clients |  Traditional CMS
:-------------------------------------------- | :-------------------: | :---------------: | :----------------:
Manages existing (custom-schema) databases    | **✓**                 | **✓**             | ✗
Works for non-website projects                | **✓**                 | **✓**             | ✗
Write simple SQL queries                      | **✓**                 | **✓**             | ✗
Granular table/field user permissions         | **✓**                 | ✗                 | ✗<sup>✝</sup>
Intuitive for non-developers                  | **✓**                 | ✗                 | **✓**<sup>✝✝</sup>
Interface for relational data                 | **✓**                 | ✗                 | **✓**
Interface for files/media                     | **✓**                 | ✗                 | **✓**
Data API                                      | **✓**                 | ✗                 | **✓**
Free and open-source                          | **✓**                 | **✓**             | **✓**

<sup>✝</sup>High-level user permissions only<br>
<sup>✝✝</sup>Often requires significant explanation or training

