---
layout: post
title: "testing out octopress"
date: 2012-09-30 21:18
comments: true
categories:  experiments
---

Blah blah, some code


{% codeblock thing lang:scala%}

val response = new DefaultHttpResponse(HTTP_1_1, OK)
val mtype = exts.get(file.toString.split('.').last).getOrElse("application/octet-stream")
response.setStatus(OK)
response.setHeader("Content-Type", mtype)
response.setContent(copiedBuffer(b))

{% endcodeblock %}


