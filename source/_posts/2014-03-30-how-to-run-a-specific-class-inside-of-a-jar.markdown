---
layout: post
title: "How to Run a Specific Class Inside of a JAR"
date: 2014-03-30 20:34:47 -0500
comments: true
categories: [Java]
---

My friend wanted me to test out his program, but it didn't have a main class specified in the manifest. Here's the solution:

```
java  -cp yourjar.jar com.yourpackage.YourClass
```

This will run the specified class as the main class.

Source: [StackOverflow](http://stackoverflow.com/questions/5474666/how-to-run-a-class-from-jar-which-is-not-the-main-class-in-its-manifest-file)
