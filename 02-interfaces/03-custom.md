# Custom User Interfaces (UIs)

## UI Structure
For most content types the Directus Core User-Interfaces should work well. However if you're looking for a specific interface or have proprietary or custom content types to manage – you may need or want to create something more tailored. Directus UIs are modular Javascript files (or dedicated sub-directories for complex interfaces) that allow you to create new ways of interfacing with database content.

Text inputs, checkboxes, and WYSIWYG editors are pretty standard – but perhaps your application needs a JSON editor, unique hashtag generator, iTunes song lookup, or custom seating-chart. So let's look at how these would be created within Directus, starting with the components of the UI.

### ID
Each UI must have a unique identifier. For instance the Single File ID is `single_file`.

### Datatypes
Each UI works with a specific set of datatypes, for instance a _Text Area_ UI might work with `TEXT` or `VARCHAR` datatypes, while a _Single File_ UI only works with `INT` (storing the related file ID).

### Options
Options are the key to making the UI usable in different circumstances. Options are easy to create, and actually use OTHER UIs as the interface for setting the value (so meta). Below is an example of an dropdown option to determine the size of an interface:

```
{id: 'size', ui: 'select', required: true, options: {options: {'large':'Large','medium':'Medium','small':'Small'} }, comment: "Choose a size!"},
```

### Template
Whether it's simple enough to add (escaped) in the single Javascript file, or to be included from a separate template file – this is where you define your markup and any additional styling. Directus uses the Handlebars templating library – so be sure to reference their Docs for any questions you may have.

### Listing
In addition to how the content is manipulated on the Edit Item page, you also need to consider how the data will be presented on the Item Listing page (more tabular). Each UI has a separate `list` function to handle that view.

### Validation
Of course you're going to want to ensure that data is saved correctly into the column – so you should always include logic in the `validate` function.

## Creating Your First UI
The easiest way to get started is to take one of the existing Core UIs and duplicate it. If possible, try to find one with similar functionality that supports the same datatype(s). Here are the steps for using an existing UI as a starter template to create your new UI:

1. Copy a Core UI file from `/app/core/uis` into the custom UI directory: `/customs/uis`, giving it a new name.
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

## Example UI
As an example we are going to create a _Text Area_ with a limited character-count, and will update the remaining characters as the user add or remove characters from the interface.

UIs depends on two objects, `UIComponent` and `CustomUIView` (optionally).

- **UIComponent** is the base object for a UI. It takes care of the validation, representation values, its Input view (UIView), and everything in between.

- **CustomUIView** is a Backbone.View object that represents the Input, what the user will see while editing an entry. Anything you can do on a Backbone View you can do in the UIView. To be more specific, here we are extending from [Backbone Layout Manager](https://github.com/tbranyen/backbone.layoutmanager) which extends the Backbone View, so anything that backbone.layoutmanager does you can do it too. _**Note**_: `CustomUIView` is the same as `UIView` the only difference is that the template prefix is set to `customs/uis/` instead of `app/core/uis`.

### Input
```js
define(['core/UIComponent', 'core/CustomUIView'], function(UIComponent, UIView) {
	var charactersLimit = 100;
	var Input = UIView.extend({
		templateSource: '<textarea maxLength="{{maxLength}}"></textarea><span id="count">{{charactersRemaining}}</span>',
		events: {
			'keyup textarea': 'updateCount'
		},
		updateCount: function(event) {
			var textLength = event.currentTarget.value.length;
			var textRemaining = charactersLimit - textLength;
			this.$el.find('#count').text(textRemaining);
		},
		serialize: function() {
			return {
				maxLength: charactersLimit,
				charactersRemaining: charactersLimit
			}
		}
	});
});
```

#### Template Source
Template source can be any valid [Handlebars](http://handlebarsjs.com) source, which include plain HTML and CSS. For larger or more complex UIs you may wish to include a separate template file instead of escaping the markup in Javascript.

#### Events
We can bind events to any element inside the UIView but we cannot bind to elements outside the view. If for some reason you want to bind to a element outside, you can use the global jquery object `$`.

Listening to `keyup` events on the text area will execute `updateCount` method.

#### Update Count
The **uppdateCount** method will execute every time the user enter characters in the text area and updates the counter.

#### Serialize
The **serialize** method returns the data that is going used when **templateSource** is rendered.

### Component
```js
var Component = UIComponent.extend({
	id: 'textlimit',
	dataTypes: ['TEXT'],
	Input: Input
});
```


#### ID
**id** is the UI's unique name.

#### Data Types
**dataTypes** are the supported data types for the UI. In this case we want to support only `TEXT` column type. The first value here is the default.

#### Input
This is the input view for the component.

### Complete UI code
```js
define(['core/UIComponent', 'core/CustomUIView'], function(UIComponent, UIView) {
	var charactersLimit = 100;
	var Input = UIView.extend({
		templateSource: '<textarea maxLength="{{maxLength}}"></textarea><span id="count">{{charactersRemaining}}</span>',
		events: {
			'keyup textarea': 'updateCount'
		},
		updateCount: function(event) {
			var textLength = event.currentTarget.value.length;
			var textRemaining = charactersLimit - textLength;
			this.$el.find('#count').text(textRemaining);
		},
		serialize: function() {
			return {
				maxLength: charactersLimit,
				charactersRemaining: charactersLimit
			}
		}
	});

	var Component = UIComponent.extend({
		id: 'textlimit',
		dataTypes: ['TEXT'],
		Input: Input
	});

	return Component;
});
```

### Enabling an UI
To use a UI simply copy it into your `/customs/uis` directory.

## UI Options
In the [previous section](05-custom-uis/01-create-an-ui.md) we explained how to create a UI that limits how many characters they can type into a text area while showing the characters remaining.

In the example, we directly create a variable with a 100 character limit – but what if this limit is changed? What if you want to use different limit on a different field? The solution to this is UI options.

UI options are settings for each interface found within the Setting panel. These values are not shared between UIs, but are specific to each column.

### Adding options
Add a new property inside **Component** object named `variables`.

**variables** property is an array of objects that will each represent a setting inside the column settings editor.

### Options structure
The structure of each option is the following:

```js
{
	id: 'option-id',
	ui: 'textinput',
	default_value: 'default_value',
	comment: 'This is a comment for this ui setting'
}
```

Now let's add a new option for our Text Area characters limitation UI:
```js
var Component = UIComponent.extend({
		id: 'textlimit',
		dataTypes: ['TEXT'],
		variables: [
			{id: 'characters_limit', ui: 'numeric', default_value: 100, comment: 'Characters Limitation'}
		],
		Input: Input
	});
```

### Result
```js
define(['core/UIComponent', 'core/CustomUIView'], function(UIComponent, UIView) {
	var Input = UIView.extend({
		templateSource: '<textarea maxLength="{{maxLength}}"></textarea><span id="count">{{charactersRemaining}}</span>',
		events: {
			'keyup textarea': 'updateCount'
		},
		updateCount: function(event) {
			var charactersLimit = this.options.settings.get('characters_limit');
			var textLength = event.currentTarget.value.length;
			var textRemaining = charactersLimit - textLength;
			this.$el.find('#count').text(textRemaining);
		},
		serialize: function() {
			var charactersLimit = this.options.settings.get('characters_limit');
			return {
				maxLength: charactersLimit,
				charactersRemaining: charactersLimit
			}
		}
	});

	var Component = UIComponent.extend({
		id: 'textlimit',
		dataTypes: ['TEXT'],
		variables: [
			{id: 'characters_limit', ui: 'numeric', default_value: 100, comment: 'Characters Limitation'}
		],
		Input: Input
	});

	return Component;
});
```
