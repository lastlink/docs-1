
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


### How do I connect my website or app?
The short answer is: however you want!

Directus only manages the content in your database, beyond that you can use whatever technologies best fit your project. Not accustomed to so much freedom? Here are three easy ways to access your data:

* **API**: Use the Directus API to fetch data as JSON
* **Directus Library**: Use the directus library of functions to interact with the database
* **SQL Queries**: Ignore Directus altogether, connect directly to the database, and use custom SQL queries

### Or don't connect anything at all!
With the ability to create and manage any database schema you can dream up, maybe Directus **is** the project. Instead of paying $20/month for a rigid Project Management service, just throw together a quick schema with fields customized to your needs. Now you have a free solution that can easily grow to accommodate any new info you want to track.

```
database
├── projects
│   ├── id
│   ├── active
│   ├── title
│   ├── description
│   ├── url
│   ├── client
│   ├── date_started
│   ├── project_manager
│   └── sow_pdf
├── clients
│   ├── id
│   ├── logo_image
│   ├── name
│   ├── hourly_rate
│   ├── point_of_contact_email
│   ├── point_of_contact_name
│   └── point_of_contact_phone
├── tasks
│   ├── id
│   ├── active
│   ├── sort
│   ├── title
│   ├── category
│   ├── assigned_user
│   ├── created_by
│   ├── date_created
│   └── description
├── task_categories
│   ├── id
│   └── title
└── project_tasks (junction table)
    ├── id
    ├── project_id
    └── task_id
```
