title: "The benefit of destructuring function arguments in ES6"
date: 2015-09-28 15:32:27
tags:
- es6
- javascript
---

ES6 brings a lot of great features to JavaScript to make it a much more modern and powerful language to work with. The days of "JavaScript sucks because it was only built in a week" have passed. One really great feature in ES6 is destructuring.

In statically typed languages, one can easily know what arguments are needed in a function by the types passed into it. For example, in Java, the following function definition is very clear:

```
public void sendMessage(Target target, String message);

```

It's obvious that the receiver of a message should be a target. In a modern IDE, calls like `sendMessage(user, msg)` would obviously send messages to a `Target`, as it is known that `user` would be part of a certain class.

However, in JavaScript or other dynamically typed languages, things are a little harder to decipher. `user` may be a user id, a user object, a username, etc.

Furthermore, `user` is a variable name, so literally anything can be passed in. A call like `sendMessage(first, s)` can be tricky to understand.

It's also pretty easy to swap the positions of variables, and there is no compiler to check if you are sending in the correct arguments.

## The Solution

One way I've found to solve this problem using ES6 is function argument destructuring.

In ES5, a function may look like this:

```
function sendMessage(target, msg) { /* ... */ }

sendMessage(usr, "Hello");
```

The same function using argument destructuring would look like this:

```
function sendMessage({ target, msg }) { /* ... */ }

sendMessage({ target: usr, msg: "Hello" });
```

Intent is much more clear in the second version than the first. This is very useful if you have many arguments to functions. If some are optional, you don't even have to pass in every single argument, as arguments are not positional. For example:

```
function sendMessage({ target, msg, notifySms = false, notifyEmail = false }) { /* ... */ }

sendMessage({ target: usr, msg: "Hello" });
sendMessage({ target: other, msg: "Look at your phone", notifySms: true });
sendMessage({ target: other, msg: "Look at your email", notifyEmail: true });
```

Now you can easily pass options into your functions without function calls having a lot of falsy/nil values.
