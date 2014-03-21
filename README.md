# [CrazyGlue] (https://github.com/defunkt/CrazyGlue)

A light-weight, bi-directional binding of DOM tag values and JS objects.
 - The tag value changes when you change the JS value.
 - The JS value changes when the tag value changes.
 - Callback for when the tag value changes.

CrazyGlue abstracts away the details of getting and setting DOM tag values,
and it provides a clean callback for when they change.
Your resulting code can thereby be cleaner, clearer and shorter.

CrazyGlue is easy to customize or monkey patch for specialized needs.

## How to install
```sh
bower install git://github.com/eddyystop/CrazyGlue
```

## Usage

#### 1. Bind to an INPUT tag (neither checkbox nor radio)
```html
<input type="text" id="the_name" value="Barbara">
```
```js
var name = new CrazyGlue('#the_name');
// name.value => 'Barbara'

name.change('John');
// document.getElementById('name') => 'John'
// name.value => 'John'
```
The JS object `name` is bound with the `<input>` tag.
`name.value` is set to the tag's current value.
`name.change(newValue)` changes the tag and object values.
`name.value` is updated whenever the tag value changes (via 'change' event).

```js
var name = new CrazyGlue('#the_name', function (value) {
// value, name.value => tag's new value
});
```
The callback is called whenever the tag value changes.

```js
var name = CrazyGlue('#the_name', 'John', function (value) {});
// document.getElementById('name') => 'John'
// name.value => 'John'
```
The tag value is changed during the binding.

```js
name.sync();
```
`name.value` is forced to the tag value.
You could use this after changing the tag value
without causing a 'change' event.


***


#### 2. Bind to a SELECT tag.
```html
<select id="the_club" multiple>
  <option value="club0" selected>club0 name</option>
  <option value="club2"         >club2 name</option>
  <option value="club4" selected>club4 name</option>
</select>
```
```js
var club = CrazyGlue('#the_club');
// club.value => ['club0', 'club4']

club.change(['club0', 'club2']);
// 'club0 name' and 'club2 name' are selected.
// club.value => ['club0', 'club2']
```


***


#### 3. Bind to radio buttons.
```html
<input type="radio" name="sex" value="male">Male
<input type="radio" name="sex" value="female">Female
```
```js
var sex = new CrazyGlue('input:radio[name=sex]');
// sex.value => []

sex.change('male');
```


***


#### 4. Bind to checkbox.
```html
<input type="checkbox" name="animal" value="dog">Dog<br>
<input type="checkbox" name="animal" value="cat" checked>Cat
```
```js
var sex = new CrazyGlue('input:checkbox[name=animal]');
// animal.value => ['cat']

animal.change('dog');
```


***


#### 5. Consistent value types
The SELECT, checkbox and radio button `.value` is always an array.
- No selection => []
- One selection => ['val']
- Multiple selections => ['val1', 'val2']

Their `.change(newValue)` may be a string, an array, null, or undefined.

The `.value` for other INPUT types is always a string, perhaps empty.
Their `.change(newValue)` may be a string, null, or undefined.

## Dependencies
- Requires jQuery 1.7+.

Note: CrazyGlue uses the native (non jQuery) `change` event.

## License
Copyright (c) 2014 John Szwaronek (<johnsz9999@gmail.com>).
Distributed under the MIT license. See LICENSE.md for details.