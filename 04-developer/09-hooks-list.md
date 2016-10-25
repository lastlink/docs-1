# Hooks

Hooks allow you to _hook_ function to be called in a specific time during the executing of Directus.

## Hooks list

Name                    | Description
----------------------- | ------------
application.boot        | When the API start booting. Before all endpoints are being set. app object is passed.
application.init        | API has booted but the endpoint hasn't been dispatched. app object is passed.
application.shutdown    | API has ran and it's about to shutdown. app object is passed.
application.error       | An Error has occurred. Exception object is passed.
directus.authenticated  | User has been authenticated. app object and user info (array) is passed.
directus.authenticated.token  | User has been authenticated through the **API**. app object and user info (array) is passed.
directus.authenticated.admin  | User has been authenticated through the **Web App**. app object and user info (array) is passed.
directus.start          | User has been authenticated and API is about to start. app object is passed.
table.create:before     | Before a table is being created. Table name passed.
table.create:after      | After a table has been created. Table name passed.
table.create            | Alias for table.create:after
table.drop:before       | Before a table is being dropped. Table name is passed.
table.drop:after        | After a table has been dropped. Table name is passed.
table.drop              | Alias for table.drop:after
table.insert:before     | Before new record is being added to a table. Table name and record data passed.
table.insert:after      | After new record has been added to a table. Table name and record data inserted passed.
table.insert            | Alias for table.insert:after
table.insert.[table-name]:before     | Before new record is being added to [table-name]. Record data passed.
table.insert.[table-name]:after      | After new record has been added to [table-name]. Record data inserted passed.
table.insert.[table-name]            | Alias for table.insert.[table-name]:after
table.update:before     | Before a table record is being updated. Table name and record data passed.
table.update:after      | After a table record has been updated. Table name and record data passed.
table.update            | Alias for table.update:after
table.update.[table-name]:before     | Before a [table-name] record is being updated. Record data passed.
table.update.[table-name]:after      | After a [table-name] record has been updated. Record data passed.
table.update.[table-name]            | Alias for table.update.[table-name]:after
table.delete:before     | Before a table record is being deleted. Table name passed.
table.delete:after      | After a table record has been deleted. Table name.
table.delete            | Alias for table.delete:after
table.delete.[table-name]:before     | Before a [table-name] record is being deleted.
table.delete.[table-name]:after      | After a [table-name] record has been deleted.
table.delete.[table-name]            | Alias for table.delete.[table-name]:after
files.saving            | Before a file is being save. Filename and size is passed.
files.saving:after      | After a file has been saved. Filename and size is passed.
files.thumbnail.saving            | Before a file thumbnail is being saved. Filename and size is passed.
files.thumbnail.saving:after      | After a file thumbnail has been saved. Filename and size is passed.
files.deleting            | Before a file is being deleted. File info is passed.
files.deleting:after      | After a file has been deleted. File info is passed.
files.thumbnail.deleting            | Before a file thumbnail is being deleted. File info is passed.
files.thumbnail.deleting:after      | After a file thumbnail has been deleted. File info is passed.
directus.index.start    | Index page starts.
directus.login.start    | Login page starts.
