---
layout: post
title: "How to Change the Name of the JAR Produced in Gradle"
date: 2014-03-31 23:19:07 -0500
comments: true
categories: [Gradle]
---

I don't like the traditional JAR name assigned in Gradle. In Bukkit development, you usually make the JAR name the same as the plugin name. Here's how you set the name of the JAR:

```
jar.baseName = 'JarName'
```

Where `JarName` would be the name of the jar generated in `build/libs/`.

Source: [StackOverflow](http://stackoverflow.com/questions/6768295/gradle-jar-file-name-in-java-plugin)
