title: "Using form-horizontal with simple_form in Rails 4"
date: 2015-04-23 14:14:44
tags: [rails, web]
---

[simple_form][1] is a really great gem for generating bootstrap forms. However, you have to
do a little extra to get it working with [Bootstrap's][2] `form-horizontal` class. The
README doesn't mention this, but it's built in. Just write your form declaration like this:

```
<%= simple_form_for [:admin, @c], html: { class: 'form-horizontal' },
  wrapper: :horizontal_form do |f| %>

# ...form...

<% end %>
```

Note the `wrapper` attribute. This isn't described in the README, and I had to dig through the
code to figure it out.

Hope this helps someone!

[1]: https://github.com/plataformatec/simple_form
[2]: http://getbootstrap.com/
