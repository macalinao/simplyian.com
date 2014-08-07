---
layout: post
title: "JSON Backends Are The Next Big Thing"
date: 2014-08-07 12:19:32 -0500
comments: true
categories: [Web]
---

[AngularJS](http://angularjs.org) is an awesome web framework made by Google
to create "structured web apps". In this framework, templating is done client-side,
so all the server needs to do is send data to the client via HTTP. Thus, no templating
needs to be done on the backend and the web browser handles all of the data.
All the backend needs to do is send JSON.

This is awesome.

Why? Because data is now separate from the view. Model-View-Controller, or MVC for
short, has long been a standard of developing web applications as it organizes code
in a way that just makes sense. A controller takes a request and serves a model, the
data, and a view, which formats the data into a nice format.

However, since the introduction of the iPhone, web isn't all we have to worry about.
Mobile apps are becoming almost necessary for services. Everyone does things from
their phone now, as not everyone wants to bring a laptop around everywhere they go.

Websites are not built for mobile devices. Yes, there is responsive web design, but
that does not beat the usefulness of an app that you can just click from your home
screen. Thus, apps are a necessity.

So let's say you built a backend specific for your app. Great! But how about if you
need to deal with other platforms? For example, smart watches or smart TVs. You need
to build a whole new app that may have a completely different interface. To make this
easier, you can create an API which will make it easy to interface with your website.
You can even expose this API to developers to increase adoption of your product.

However, now you have this website that you simultaneously have to maintain. Every
new feature of the website has its own rendering mechanism completely separate from
the REST API. The features of the REST API aren't synchronized with your website.

Here's where frameworks like Angular come in. Angular can be like a mobile app,
dealing directly with your API. When you build a new feature on your website, you
can also build the logic into your API, causing you to only have to write your code
ONCE. Now you don't have to worry about supporting certain operations on multiple
platforms, as you have one backend that handles all of the platforms.

JSON-based backends are awesome. Logic is written once, and all you have to worry about
is how your data is displayed. You can still support multiple platforms, but you only
need to write your backend logic once, as JSON is ubiquitous.
