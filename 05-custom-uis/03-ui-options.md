# UI Options
In the [previous chapter](05-custom-uis/01-create-an-ui.md) we explain how to create an UI that limits the users on how many characters can they type in a text area while showing the remaining characters.

In the example we directly create a variable with a limitation of 100 characters, what if this limitation changed? what if you want to use different limitation on different field you may ask? the solution to this is using UI options.
 
UI options are settings used on each field in the columns settings section. These options values are not shared between UIs, but only for an specific field.

### Adding options
Add a new property inside **Component** object named `variables`.

**variables** property is a array of object that each will represents a settings inside this column in the column settings editor.

### Options structure
the structure of each options is the following:

```js
{
  id: 'option-id',
  ui: 'textinput',
  default_value: 'default_value',
  comment: 'This is a comment for this ui setting'
}
```

Now let's add a new option for our new Text Area characters limitation UI.
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

## Result

```js
define(['core/UIComponent', 'core/UIView'], function(UIComponent, UIView) {
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
