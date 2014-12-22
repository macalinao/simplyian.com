title: Creating a Todo app on the MEAN stack using Preston
date: 2014-12-20 18:34:19
tags:
- preston
- rest
- MEAN
- Node.js
---

[Preston][preston] is an extremely powerful library for creating RESTful applications that use Mongoose models. In this tutorial, I'll be hooking up the [AngularJS TodoMVC app][angular-todomvc] to a Preston-powered backend.

First, I've created a repo that is based off of the AngularJS Todo app. You can clone the first step like so:

```
git clone https://github.com/simplyianm/todomvc-preston-angular.git
git checkout angular
```

This is the TodoMVC app with a few changes for simplicity:

1. It uses a CDN rather than Bower.
2. It uses Express to serve the app rather than being static HTML. This makes the differences between pure Angular to Angular+Preston much more pronounced.

## Backend

To create our backend, we must first install Mongoose, Preston, and [body-parser][body-parser] like so:

```
npm install --save preston mongoose
```

Once this is done, we're ready to start writing the code for our app. We'll write all of our backend code in `app.js`. First, let's require Mongoose and Preston, so we can use them in our code.

```
var mongoose = require('mongoose');
var preston = require('preston');
```

Next, let's connect to our MongoDB database. I'm using MongoHQ since this will be on Heroku, but you can use whatever MongoDB database you want.

```
mongoose.connect(process.env.MONGOHQ_URL || 'mongodb://localhost:27017');
```

Once Mongoose is connected, let's define our model for our todos. We can define it like so:

```
var Todo = mongoose.model('Todo', new mongoose.Schema({
  title: String,
  completed: Boolean
}));
```

Next, let's add Preston into this. There are only three lines of code needed to create a fully functional JSON RESTful backend with Preston:

```
app.use(require('body-parser').json());
preston(Todo);
app.use('/api', preston.middleware());
```

The first line of code is required to parse the JSON request bodies which Preston depends on.

The second line of code tells Preston that we want to create routes for the `Todo` model. By default, all 5 methods (query, create, get, update, destroy) are exposed with full access. *Note: if you don't want this in your own application, Preston has the power to control what gets sent in every one of those methods. [Read the docs][preston-gh] for more details.

The last line tells Express to serve any registered models on the `/api` route. Thus, routes under `/api/todos` are created.

We're going to add one more line of code to show what routes are created, for the sake of example:

```
preston.printRoutes();
```

This just prints all generated routes, without their prefixes.

## Frontend (Angular)

Fortunately, most of the AngularJS app is done. The TodoMVC example provides a sample connection to a sample RESTful backend (like ours). This is part of what makes Preston so powerful -- **it speaks the universal language of REST.** There are tons of libraries out there to interface with REST: [Restangular][restangular], [restmod][restmod], etc.

To get the frontend working, you must populate the todos list and ignore the 404 check. You can do this with the following:

In `client/js/services/todoStorage.js`, make the `todoStorage` factory return the following:

```
return $injector.get('api');
```

In `client/js/app.js`, make the `resolve.store` function return `todoStorage`. Furthermore, add the following to `TodoCtrl`:

```
$http.get('/api/todos').then(function(data) {
  data.data.map(function(todo) {
    store.todos.push(todo);
  });
});
```

Don't forget to inject `$http` into the controller. [The entire diff of these changes can be found here.][diff] If you were too lazy to follow this tutorial, you can also type `git checkout master` into your terminal to get to the latest version.

If you're hosting the app on Heroku, you'll also need to type `heroku addons:add mongohq` to get a database hooked up to your code.

The entire backend is now hooked up to Angular with little effort. [Try it here!][heroku]

## Conclusion

Preston is a very powerful tool when used in conjunction with AngularJS. It can decrease the time it takes to get from idea to MVP significantly, as the backend code needed is extremely minimal. Preston solves the problem of creating a bunch of routes for your database whenever you need to create a model, as Preston just creates the most optimal routes and knows what you want.

In the future, I'll write about using Preston with [Restangular][restangular], as the combination is even more powerful than using `$http` alone.

[preston]: http://prestonjs.com
[preston-gh]: https://github.com/simplyianm/preston
[angular-todomvc]: http://todomvc.com/examples/angularjs/#/
[body-parser]: https://github.com/expressjs/body-parser
[restangular]: https://github.com/mgonto/restangular
[restmod]: https://github.com/platanus/angular-restmod
[diff]: https://github.com/simplyianm/todomvc-preston-angular/commit/40ddf0212a252f99dc2974b3e6c63e4c8cfe5b48
[heroku]:  https://todomvc-preston-angular.herokuapp.com/
