# Custom User Interfaces
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