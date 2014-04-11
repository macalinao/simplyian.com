---
layout: post
title: "Including Dependencies in Your Gradle Build Script's Classpath"
date: 2014-04-10 23:00:18 -0500
comments: true
categories: [Gradle]
---

In a [recent project](https://github.com/simplyianm/bukkit-bootstrap), I wanted to use SnakeYAML in my Gradle build script. This is pretty easy to do; all you have to do is add the following to your script:

```
buildscript {
    repositories {
        mavenCentral()
        // ...etc
    }

    dependencies {
        classpath group: 'org.yaml', name: 'snakeyaml', version: '1.5'
        // ..etc
    }
}
```

This is the same as the `repositories {}` and `dependencies {}` sections of the build script. After doing this, feel free to use your libraries anywhere in your build script. Don't forget to import the classes you use!

