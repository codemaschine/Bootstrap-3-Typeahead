# Bootstrap 3 Typeahead

---

For simple autocomplete use cases there seems to be nothing wrong with the dropped typeahead plugin. Here you will find the typeahead autocomplete plugin for Twitter's Bootstrap 2 ready to use with Twitter's Bootstrap 3. The original code is written by [@mdo](http://twitter.com/mdo) and [@fat](http://twitter.com/fat).

Users who migrate their website or app from Twitter's Bootstrap 2 to Bootstrap 3 can also use this plugin to keep their current autocomplete functions. See for a complete list of migrations steps: [Migrate your templates from Twitter Bootstrap 2.x to Twitter Bootstrap 3](http://bassjobsen.weblogs.fm/migrate-your-templates-from-twitter-bootstrap-2-x-to-twitter-bootstrap-3/)

With Twitter Bootstrap 3 the typeahead plugin had been dropped. [@mdo](http://twitter.com/mdo) says: "in favor of folks using [Twitter's typeahead](https://github.com/twitter/typeahead.js). Twitter's typeahead has more features than the old bootstrap-typeahead.js and less bugs." Twitter's typeahead don't work direct with Bootstrap 3. The DOM structure of the dropdown menu used by `typeahead.js` differs from the DOM structure of the Bootstrap dropdown menu. You'll need to load some additional CSS in order to get the `typeahead.js` dropdown menu to fit the default Bootstrap theme. Try [extended Bootstrap LESS](https://github.com/bassjobsen/typeahead.js-bootstrap-css) or if your are looking for a more extended version try: [typeahead.js-bootstrap3.less](https://github.com/hyspace/typeahead.js-bootstrap3.less/blob/master/typeahead.less).

~~`Typeahead.js` doesn't seem ready for the new Twitter Bootstrap 3 at the moment. Code is not up to date and fixes are needed. See also:
[Typeahead problems with Bootstrap 3.0 RC1](http://stackoverflow.com/questions/18167246/typeahead-problems-with-bootstrap-3-0-rc1).~~

## Bootstrap 4

---

[Bootstrap 4](http://blog.getbootstrap.com/2015/08/19/bootstrap-4-alpha/) is coming soon. The Bootstrap 3 Typeahead will also work with Bootstrap 4.
The look and feel of Bootstrap 4 will differ from Bootstrap 3 and so does the drop down menu. In Bootstrap 4 the typeahead dropdown menu will look like that shown in the figure below:
![Bootstrap 4 Typeahead](typeaheadv4.png).

## Download

---

- Download the latest [bootstrap3-typeahead.js](https://github.com/bassjobsen/Bootstrap-3-Typeahead/blob/master/bootstrap3-typeahead.js) or [bootstrap3-typeahead.min.js](https://github.com/bassjobsen/Bootstrap-3-Typeahead/blob/master/bootstrap3-typeahead.min.js).

- Include it in your source after jQuery and Bootstrap's JavaScript.

## Full integration with Bootstrap 3 Typeahead

---

Download the latest version of Boostrap from [Bootstrap](https://github.com/twbs/bootstrap/archive/master.zip). Copy `bootstrap3-typeahead.js` to the js/ folder. Edit `gruntfile.js` and add `bootstrap3-typeahead.js` to the plugins list.
Build your own version with typeahead with `grunt dist`.

## CSS

---

There is no additional CSS required to use the plugin. Bootstrap's CSS contains all required styles in the `.dropdown-menu` class. The original CSS adds a `z-index` of 1051 to the dropdownmenu via the typeahead class. You could add this if you need it.
`.typeahead { z-index: 1051; }` (less or css).

## Usage

---

```
<input type="text" class="typeahead" data-provide="typeahead">
```

You'll want to set `autocomplete="off"` to prevent default browser menus from appearing over the Bootstrap typeahead dropdown.

### Via data attributes

Add data attributes to register an element with typeahead functionality as shown in the example above.

### Via JavaScript

Call the typeahead manually with:

```js
$('.typeahead').typeahead()
```

Destroys previously initialized typeaheads. This entails reverting DOM modifications and removing event handlers:

```js
$('.typeahead').typeahead('destroy')
```

## Javascript Example

---

### Loading a collection

```js
$.get("example_collection.json", function(data){
  $("#name").typeahead({ source:data });
},'json');
//example_collection.json
// ["item1","item2","item3"]
```

### Using JSON objects instead of simple strings

You can add all the properties you wish on your objects, as long as you provide a "name" attribute OR you provide your own displayText method. The other values allow you to match the selected item with something in your model.

```js
var $input = $(".typeahead");
$input.typeahead({
  source: [
    {id: "someId1", name: "Display name 1"},
    {id: "someId2", name: "Display name 2"}
  ],
  autoSelect: true
});
$input.change(function() {
  var current = $input.typeahead("getActive");
  if (current) {
    // Some item from your model is active!
    if (current.name == $input.val()) {
      // This means the exact match is found. Use toLowerCase() if you want case insensitive match.
    } else {
      // This means it is only a partial match, you can either add a new item
      // or take the active if you don't want new items
    }
  } else {
    // Nothing is active so it is a new value (or maybe empty value)
  }
});
```

## Options

---

Options can be passed via data attributes or JavaScript. For data attributes, append the option name to `data-`, as in `data-source=""`.

If you are using jQuery in your application, note that camel case attributes such as `data-minLength` should be formatted as `data-min-length`. If you want more explanation, see [this issue](https://github.com/bassjobsen/Bootstrap-3-Typeahead/issues/28).

|Name|Type|Default|Description|
|--- |--- |--- |--- |
|source|array, function|`[]`|The data source to query against. May be an array of strings, an array of JSON object with a name property or a function. The function accepts two arguments, the query value in the input field and the process callback. The function may be used synchronously by returning the data source directly or asynchronously via the process callback's single argument.|
|items|number|`8`|The max number of items to display in the dropdown. Can also be set to 'all'|
|minLength|number|`1`|The minimum character length needed before triggering autocomplete suggestions. You can set it to 0 so suggestion are shown even when there is no text when lookup function is called.|
|showHintOnFocus|boolean, `"all"` or `"addItem"`|`false`|If hints should be shown as soon as the input gets focus. If set to true, all match will be shown. If set to `"all"`, it will display all hints, not filtering them by the current text. This can be used when you want an input that behaves a bit like a combo box plus auto completion as you type to filter the choices. If it is set to `"addItem"`, only the items from the addItem option will be displayed if the query is empty.|
|scrollHeight|number, function|`0`|Number of pixels the scrollable parent container scrolled down (scrolled out the viewport).|
|matcher|function|case insensitive|The method used to determine if a query matches an item. Accepts a single argument, the item against which to test the query. Access the current query with this.query. Return a boolean true if query is a match.|
|sorter|function|exact match, case sensitive, case insensitive|Method used to sort autocomplete results. Accepts a single argument items and has the scope of the typeahead instance. Reference the current query with this.query.|
|updater|function|returns selected item|The method used to return selected item. Accepts a single argument, the item and has the scope of the typeahead instance.|
|highlighter|function|highlights all default matches|Method used to highlight autocomplete results. Accepts a single argument item and has the scope of the typeahead instance. Should return html.|
|displayText|function|`item.name \|\| item`|Method used to get textual representation of an item of the sources. Accepts a single argument item and has the scope of the typeahead instance. Should return a String.|
|autoSelect|boolean|`false`|Allows you to dictate whether or not the first suggestion is selected automatically. Turning autoselect off also means that the input won't clear if nothing is selected and enter or tab is hit.|
|afterSelect|function|`$.noop()`|Call back function to execute after selected an item. It gets the current active item in parameter if any.|
|delay|integer|`0`|Adds a delay between lookups.|
|appendTo|jQuery element|`null`|By defaut, the menu is added right after the input element. Use this option to add the menu to another div. It should not be used if you want to use bootstrap dropup or dropdown-menu-right classes.|
|fitToElement|boolean|`false`|Set to true if you want the menu to be the same size than the input it is attached to.|
|addItem|JSON object or function(query): item[]\|item|`false`|Adds an item to the end of the list, for example "New Entry". This could be used, for example, to pop a dialog when an item is not found in the list of data. Example: http://cl.ly/image/2u170I1q1G3A/addItem.png|
|changeInputOnSelect|boolean|`true`|Put the selected value text representation in the input|
|changeInputOnMove|boolean|`true`|Put the active value text representation in the input|
|openLinkInNewTab|boolean|`false`|Open links in a new window/tab|
|selectOnBlur|boolean|`false`|Automatically select the active value on blur|
|showCategoryHeader|boolean|`true`|Show categories header in the dropdown menu|

## Methods

---

- `.typeahead(options)`: Initializes an input with a typeahead.
- `.lookup`: To trigger the lookup function externally
- `.getActive`: To get the currently active item, you will get a String or a JSON object depending on how you initialized typeahead. Works only for the first match.

## Bower

---

To use with [Bower](http://bower.io/). Add to your bower.json file:


```json
{
  "name": "MyProject",
  "dependencies": {
    "bootstrap3-typeahead": "git://github.com/bassjobsen/Bootstrap-3-Typeahead.git#master"
  }
}
```

## AngularJS

---

An AngularJS directive for the Bootstrap 3 Typeahead jQuery plugin can be found at https://github.com/davidkonrad/angular-bootstrap3-typeahead.

## Bloodhound

---

[Bloodhound](https://github.com/twitter/typeahead.js/blob/master/doc/bloodhound.md) is the [typeahead.js](https://github.com/twitter/typeahead.js) suggestion engine, since version 0.10.0. Bloodhound is robust, flexible, and offers advanced functionalities such as prefetching, intelligent caching, fast lookups, and backfilling with remote data. To use Bloodhound with Bootstrap-3-Typeahead:

```js
// instantiate the bloodhound suggestion engine
var numbers = new Bloodhound({
  datumTokenizer: Bloodhound.tokenizers.whitespace,
  queryTokenizer: Bloodhound.tokenizers.whitespace,
  local:  ["(A)labama","Alaska","Arizona","Arkansas","Arkansas2","Barkansas"]
});

// initialize the bloodhound suggestion engine
numbers.initialize();

$(".typeahead").typeahead({
  items: 4,
  source:numbers.ttAdapter()
});
```

## Bootstrap Tags Input

---

[Bootstrap Tags Input](http://bootstrap-tagsinput.github.io/bootstrap-tagsinput/examples/) is a jQuery plugin providing a Twitter Bootstrap user interface for managing tags. Bootstrap Tags Input has a typeahead option which allows you to set the source:

```js
$("input").tagsinput({
  typeahead: {
    source: ["Amsterdam", "Washington", "Sydney", "Beijing", "Cairo"]
  }
});
```

or

```js
$("input").tagsinput({
  typeahead: {
    source: function(query) {
      return $.get("http://someservice.com");
    }
  }
});
```

See also: https://github.com/bassjobsen/Bootstrap-3-Typeahead/issues/40
