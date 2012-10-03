---
layout: post
title: "I need to look at Sinatra..."
date: 2008-08-13 03:30
comments: false
permalink: /post/45788533/i-need-to-look-at-sinatra
categories:
---

 

The concept of combining routes and controllers makes alot of sense:
get '/user/:id/bio' do  User.find(params[:id]).bioend