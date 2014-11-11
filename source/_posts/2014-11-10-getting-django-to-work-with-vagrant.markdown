---
layout: post
title: "Getting Django To Work With Vagrant"
date: 2014-11-10 13:13:35 -0600
comments: true
categories: 
---

I was having problems getting Django working with Vagrant, then I stumbled upon this [StackOverflow answer](http://stackoverflow.com/questions/5984217/vagrants-port-forwarding-not-working).

The problem with the port forwarding is not with Vagrant, but with Django itself. You need to bind to `0.0.0.0`, not `127.0.0.1`.

So you'd run this command:

```
python migrate.py runserver 0.0.0.0:8000
```

That will fix all of your issues.

