
# What is Directus?
_Directus is a free and open-source SQL database GUI for intuitively managing your project’s content._

### So, is it a CMS or a Database Administration Tool?
As a developer, you're probably already managing content directly through Sequel-Pro, phpMyAdmin, or the command line. These are excellent tools because you get complete control with no setup other than entering the database credentials... but you would never give that access to clients, designers, or even inexperienced engineers. Handling relational ids, media/file references, and data validation just isn't intuitive at that level – let alone the risk of accidentally deleting/truncating tables.

What if you want non-technical users to manage that same database content through a simple, intuitive, and feature-rich interface – tailoring table/field access with granular permissions. Innumerable Content Management Systems probably come to mind, but typically those have steep learning curves, require complicated proprietary database schemas, and generally make assumptions about what you're doing and how to do it. On top of that, most CMS are tangled with entire website templating solutions – but maybe your database isn't even supporting a website... maybe it's for a native app, internal inventory tracking, or customizable project management. 


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

