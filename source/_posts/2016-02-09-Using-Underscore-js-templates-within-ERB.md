title: Using Underscore.js templates within ERB
date: 2016-02-09 10:11:36
tags: erb, web, underscore
---

You don't always have React to create a new feature on a website. Recently, I used Underscore and jQuery within a Rails application to create a dynamic page.

## Underscore + jQuery -> Easy templating

If you specify an unknown script type in a script tag, you can insert code blocks into your code that aren't rendered. For example, here I'll define a quick template:

``` html
<script id="myTemplate" type="text/template">
Hello, <%= target %>!
</script>
```

You can then access the contents of this script tag easily using jQuery:

``` javascript
var templateStr = $('#myTemplate').html();
```

Using Underscore, we can compile this into a template function like so:

``` javascript
var template = _.template($('#myTemplate').html())

console.log(template({ target: 'world' })) // prints 'Hello, world!'
```

With jQuery, we can render this template to the page very easily.

First, let's declare a div to render this content within:

``` html
<div id="mount"></div>
```

Then, let's write our code to render stuff:

``` javascript
var template = _.template($('#myTemplate').html());
function render() {
  $('#mount').html(template({
    target: 'world' // Of course, we can get these variables from anywhere
  }))
}
render();
```

Now, any time you want to rerender the template, you can just call "render()".

## Within Rails

The main problem with using Underscore templates within a Rails application is that ERB and Underscore by default use the same template tags, `<%` and `%>`. You can get around this by using the following code:

``` javascript
_.templateSettings = {
  interpolate: /\{\{\=(.+?)\}\}/g,
  evaluate: /\{\{(.+?)\}\}/g
};
```

This will allow you to use templates as follows:

``` html
<script type="text/template">
{{ users.forEach(function (user) { }}
    <p>{{= user.name }}
{{ }) }}
</script>
```

{% raw %}
The "interpolate" property (here set to "{{= expr }}") defines how to do interpolation (inserting values), and the "evaluate" property (here set to "{{ code }}") defines how to run arbitrary Javascript.
{% endraw %}

Next time you're unable to use modern web technologies to make a simple dynamic web page, consider this approach!
