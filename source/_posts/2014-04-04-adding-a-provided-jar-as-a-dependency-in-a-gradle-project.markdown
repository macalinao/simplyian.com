---
layout: post
title: "Adding a Provided JAR as a Dependency in a Gradle Project"
date: 2014-04-04 23:39:12 -0500
comments: true
categories: [Gradle, Java]
---

Adding a JAR as a dependency is simple in [Gradle](http://gradle.org/). In your `dependencies {}`, add the following line:

```
compile files('file.jar')
```

Where `file.jar` is the path to the JAR from the root directory of the repository. For example, if I had `Dependency.jar` at `./libs/Dependency.jar`, I would use `compile files('libs/Dependency.jar')`.
