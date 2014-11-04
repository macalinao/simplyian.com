---
layout: post
title: "The Coffeescript Keyword Nobody's Heard Of: 'by'"
date: 2014-11-04 08:22:44 -0600
comments: true
categories: 
---

Coffeescript is an amazing language. As a matter of fact, it’s one of my favorite languages, second only to JavaScript. Here’s some recent code I used to split up one array into a multidimensional array with a certain number of columns.

```coffeescript
matrix.push arr[i..(i + cols - 1)] for i in [0..arr.length - 1] by cols
```

Notice the second to last keyword: by.

The `by` keyword basically changes the increment of the generated for loop. Without the `by`, you’d have `i++` as the increment of your for loop. However, with the `by`, you’d instead have `i += 3` if you had `by 3`.

Here’s a simple example where I am getting money out of my bank account in the form of 5 dollar bills.

```coffeescript
console.log "I have #{i} dollars." for i in [0..100] by 5
```

This translates to the following Javascript:

```coffeescript
var i;
for (i = 0; i <= 100; i += 5) {
  console.log("I have " + i + " dollars.");
}
```

As you can see, the increment of the loop is now 5 rather than just 1.

Now the question is, are there any other hidden features of Coffeescript like this?
