# Create a UI

UIs depends on two objects, `UIComponent` and `BaseUIView` (optionally).

- **UIComponent** is the base object for a UI. It takes care of the validation, representation values, its Input view (UIView), and everything in between.
- **BaseUIView** is a Backbone.View object that represents the Input, what the user will see while editing an entry. Anything you can do on a Backbone View you can do in the UIView. To be more specific, here we are extending from [Backbone Layout Manager](https://github.com/tbranyen/backbone.layoutmanager) which extends the Backbone View, so anything that backbone.layoutmanager does you can do it too. _**Note**_: `BaseUIView` is the same as `UIView` the only difference is that the template prefix is set to `customs/uis/` instead of `app/core/uis`.

As an example we are going to create a _Text Area_ with a limited character-count, and will update the remaining characters as the user add or remove characters from the interface.

## Input
 
```js
define(['core/UIComponent', 'core/BaseUIView'], function(UIComponent, UIView) {
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

### Template Source
Template source can be any valid [Handlebars](http://handlebarsjs.com) source, which include plain HTML and CSS. For larger or more complex UIs you may wish to include a separate template file instead of escaping the markup in Javascript.

### Events
We can bind events to any element inside the UIView but we cannot bind to elements outside the view. If for some reason you want to bind to a element outside, you can use the global jquery object `$`.

Listening to `keyup` events on the text area will execute `updateCount` method.

### Update Count
The **uppdateCount** method will execute every time the user enter characters in the text area and updates the counter.

### Serialize
The **serialize** method returns the data that is going used when **templateSource** is rendered.

## Component

```js
var Component = UIComponent.extend({
    id: 'textlimit',
    dataTypes: ['TEXT'],
    Input: Input
});
```


### ID
**id** is the UI's unique name.

### Data Types
**dataTypes** are the supported data types for the UI. In this case we want to support only `TEXT` column type. The first value here is the default.
 
### Input
This is the input view for the component.

## Complete UI code

```js
define(['core/UIComponent', 'core/BaseUIView'], function(UIComponent, UIView) {
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

## Enabling an UI
To use this UI simply copy the file into your `/customs/uis` directory.
