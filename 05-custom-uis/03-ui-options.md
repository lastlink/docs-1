# UI Options
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

## Result

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
