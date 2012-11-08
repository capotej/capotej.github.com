---
layout: post
title: "announcing finatra 1.0.0"
date: 2012-11-07 21:20
comments: true
categories: ["finatra", "scala"]
---

After months of work [Finatra](http://github.com/capotej/finatra#readme) 1.0.0 is finally available! Finatra is a scala web framework inspired by [Sinatra](http://github.com/sinatra/sinatra#readme) built on top of [Finagle](http://twitter.github.com/finagle).

### The API

The API looks like what you'd expect, here's a simple endpoint that uses route parameters:

```scala
get("/user/:username") { request =>
  val username = request.routeParams.getOrElse("username", "default_user")
  render.plain("hello " + username).toFuture
}
```

The ```toFuture``` call means that the response is actually a [Future](http://twitter.github.com/scala_school/finagle.html#Future), a powerful concurrency abstraction worth checking out.

### A super quick demo:

```sh
$ git clone http://git@github.com:capotej/finatra.git
$ cd finatra
$ ./finatra new com.example.myapp /tmp
```

Now you have an ```/tmp/myapp``` you can use:

```sh

$ cd /tmp/myapp
$ mvn scala:run
```

A simple app should've started up locally on port 7070, verify with:

```sh
$ curl http://locahost:7070
hello world
```

You can see the rest of the endpoints at ```/tmp/myapp/src/main/scala/com/example/myapp/App.scala```



Make sure to see the full details in the [README](http://github.com/capotej/finatra#readme) and check out the [example app](http://github.com/capotej/finatra-example).

Props to [@twoism](http://twitter.com/twoism) and [@thisisfranklin](http://twitter.com/thisisfranklin) for their code, feedback and moral support.







