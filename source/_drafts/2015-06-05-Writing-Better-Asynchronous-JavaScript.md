title: "Writing Better Asynchronous JavaScript"
date: 2015-06-05 18:04:36
tags: [javascript, asynchronous]
---

One of the main benefits of JavaScript is its ability to execute asynchronously. Basically, when a function dealing with I/O is called, instead of being blocked, the engine can continue to execute other code while waiting for the operation to finish. When the operation is done, the data can be sent to another routine known as a callback.

This property of the language has made it an increasingly popular choice for server-side applications in the forms of projects such as Node.js. However, this awesome feature has a major downside -- it doesn't read well.

In a language like Ruby, you might do something like this:

```ruby
user = User.where(name: "Alice").first
user.name = "Bob"
user.save!

puts user # Prints out the updated user object
```

However, in asynchronous JavaScript, it may look like this:

```js
User.find({ name: 'Alice' }, function(err, user) {
  if (err) return;
  user.name = 'Bob';
  user.save(function(err2, doc) {
    if (err2) return;
    console.log(doc);
  });
});
```

This can get even worse:

Ruby:

```ruby
user = User.where(name: "Alice").first
user.name = "Bob"
user.save!

comment = Comment.new(user: user, content: "Hello, world!")
comment.save!

puts user
puts comment
```

JavaScript:

```js
User.find({ name: 'Alice' }, function(err, user) {
  if (err) return;
  user.name = 'Bob';
  user.save(function(err2, doc) {
    if (err2) return;
    var comment = new Comment({
      user: doc._id,
      content: 'Hello, world!'
    });
    comment.save(function(err3, doc2) {
      if (err3) return;
      console.log(doc);
      console.log(doc2);
    });
  });
});
```

This phenomenon is known as [callback hell][callback-hell]. A lot of people hate it, and a lot of people hate JavaScript because of it. Over time, people have created ways to prevent it.

## Separating code into functions

One way to make your code easier to read is by naming your functions:

```js
User.find({ name: 'Alice' }, function updateUser(err, user) {
  if (err) return;
  user.name = 'Bob';
  user.save(function saveUser(err2, doc) {
    if (err2) return;
    var comment = new Comment({
      user: doc._id,
      content: 'Hello, world!'
    });
    comment.save(function printDocs(err3, doc2) {
      if (err3) return;
      console.log(doc);
      console.log(doc2);
    });
  });
});
```

It's marginally better, sure but we can do better. In JavaScript, functions can be passed as arguments to other functions like a variable, a property called [first-class functions][fcf]. Therefore, you can modularize your code like so:

```js
function printDocs(user, comment) {
  console.log(user);
  console.log(comment);
}

function createComment(user) {
  var comment = new Comment({
    user: user._id,
    content: 'Hello, world!'
  });
  comment.save(function(err3, doc2) {
    if (err3) return;
    printDocs(user, doc2);
  });
}

User.find({ name: 'Alice' }, function updateUser(err, user) {
  if (err) return;
  user.name = 'Bob';
  user.save(function saveUser(err2, doc) {
    if (err2) return;
    createComment(doc);
  });
});
```

As you can see, it's really not much better. Vanilla JavaScript really sucks for writing clean asynchronous code. This is where libraries come into play.

## Async

[Async][async] is a great library for writing -- you guessed it -- asynchronous code.

[callback-hell]: http://callbackhell.com/
[fcf]: http://en.wikipedia.org/wiki/First-class_function
[async]: https://github.com/caolan/async
