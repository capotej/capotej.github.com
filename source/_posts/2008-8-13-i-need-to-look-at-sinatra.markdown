---
layout: post
title: "I need to look at Sinatra..."
date: 2008-08-13 03:30
comments: false
permalink: /post/45788533/i-need-to-look-at-sinatra
categories:
---

 ### I need to look at Sinatra...
August 13 2008,  3:30 AM by Julio Capote

The concept of combining routes and controllers makes alot of sense:
get '/user/:id/bio' do  User.find(params[:id]).bioend