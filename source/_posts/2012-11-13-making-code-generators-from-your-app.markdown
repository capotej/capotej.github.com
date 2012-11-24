---
layout: post
title: "automatic READMEs and more"
date: 2012-11-13 21:31
comments: true
categories: ["shell scripting", "finatra"]
published: false
---

Whenever I released a new version of [Finatra](https://github.com/capotej/finatra#readme), I always had update a few things so everything was on the latest version and code:

1) The version in the xml fragment of the main README.markdown has to change

2) The version in the pom.xml of the example app has to change

3) Any api changes, if any, have to be updated in the example app

4) The version in the template pom.xml of the app generator has to change

5) Any api changes, if any, have to be updated inside the app template

After messing this up a few times, I created a [sub](https://github.com/37signals/sub#readme) script that generates the example app, the README, *and* the app generator, straight from unit test! Here's how I did it:

## The source of truth

A common problem with code generators is the source code they generate quickly becomes out of date, because the templates aren't updated as often as the api changes in the framework. To avoid this, I made a special unit test that I'd use as the "seed" for my generator. A short example:

```scala ExampleAppSpec.scala
class ExampleSpec extends SpecHelper {

  /* ###BEGIN_APP### */

  class ExampleApp extends Controller {

    /**
     * Basic Example
     *
     * curl http://localhost:7070/hello => "hello world"
     */
    get("/") { request =>
      render.plain("hello world").toFuture
    }

  val app = new ExampleApp

  /* ###END_APP### */


  /* ###BEGIN_SPEC### */

  "GET /hello" should "respond with hello world" in {
    get("/")
    response.body should equal ("hello world")
  }

  /* ###END_SPEC### */
}
```

Using the special comments, I can extract a sample app a test suite from the source code.

## The app generator

Now that we have our "template", we can build our app generator to use it. I customized [base](http://capotej.com/blog/2012/11/01/base-a-scala-project-generator/) and ended up with: [script/finatra/libexec/finatra-new](https://github.com/capotej/finatra/blob/master/script/finatra/libexec/finatra-new)

You can then run

```sh
$ ./finatra new com.example.myapp
```

and it will generate ```myapp/``` based on the tested example code from the test suite above!

## The example app

This command uses the generator to generates/update [finatra-example](https://github.com/capotej/finatra-example)

```sh

#!/bin/bash
# Usage: finatra update-example
# Summary: generates the example app from the template

set -e

source $_FINATRA_ROOT/lib/base.sh

tmpdir=$(mktemp -d /tmp/finatra_example.XXX)

$_FINATRA_ROOT/bin/finatra new com.twitter.finatra_example $tmpdir

cp -Rv $tmpdir/finatra_example/ $EXAMPLE_REPO

rm -rf $tmpdir

cd $EXAMPLE_REPO && mvn test

```

This also has the neat side effect of testing the app generator and the generated app.

## Updating the README's

I also have a [command](https://github.com/capotej/finatra/blob/master/script/finatra/libexec/finatra-update-readme) for updating the README with fresh examples and version numbers.



