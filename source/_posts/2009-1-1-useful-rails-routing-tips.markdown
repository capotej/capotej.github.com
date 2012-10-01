---
layout: post
title: "Useful Rails Routing tips"
date: 2009-01-1 15:50
comments: false
permalink: /post/67873462/useful-rails-routing-tips
categories:
---

 # Julio Capote
## This is an archived post
This is an archived post
[Previous](../../../posts/2008/10/post/56866975/so-you-want-to-click-that-button.html)  [Index](../../../index-2.html)  [Next](../../../posts/2009/07/post/145035194/using-rack-applications-inside-gwt-hosted-mode.html) ### Useful Rails Routing tips
January  1 2009,  3:50 PM by Julio Capote

Even though I have been using Rails for fun and profit for about 2 years now, I felt I never really used it’s routing engine to its full potential. So I checked out new[Rails Routing from the outside in](http://guides.rubyonrails.org/routing_outside_in.html) guide and discovered bunch of useful tricks that I (and maybe you) had no idea you could do. Here they are:### Multiple resource definitions on a single line

map.resources :photos, :books, :videos### Impose a certain format for resource identifiers

map.resources :photos, :requirements => { :id => /[A-Z][A-Z][0-9]+/ }

This way, /photos/3 would not work, but /photos/DA321 would.### Friendlier action names


Say for your application ‘create’ and ‘change’ make more sense than the default ‘new’ and ‘edit’ you can do
map.resources :photos, :path_names => { :new => 'make', :edit => 'change' }

You can also do this site-wide also, in your environment.rb
config.action_controller.resources_path_names = { :new => 'make', :edit => 'change' }### Trim the fat off resources with :only and :except


When you use map.resources, rails generates 7 restful routes for that resource; But what if that resource only needed to be seen and listed, never edited or created?
map.resources :photos, :only => [:index, :show]

If your application uses alot of map.resources calls but not neccesarily all its generated routes, you can save memory this way.### Adding extra routes to your resources


Instead of fighting the map.resources generator by placing a horror like this atop your routes.rb
map.connect '/photos/:id/preview', { :controller => 'photos', :action => 'preview' }

You can do this to your already mapped resource
map.resources :photos, :member => { :preview => :get }

This will map all GET’s to /photos/3 to the preview action of your photos controller

This can also be  used in collections instead of singular members, just change :member to :collection
map.resources :photos, :collection => { :search => :get }

This will give you /photos/search and hit the search action within the photos controller#### 1731 views and 0 responses


