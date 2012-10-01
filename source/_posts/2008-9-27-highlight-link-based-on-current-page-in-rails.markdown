---
 layout: post
 title: "Highlight link based on current page in rails"
 date: 2008-09-27 19:47
 comments: false
 categories:
 ---

 # Julio Capote
## This is an archived post
This is an archived post
[Index](../../../index-2.html)  [Next](../../../posts/2008/09/post/52369865/i-would-buy-and-frame-this.html) ### Highlight link based on current page in rails
September 27 2008,  7:47 PM by Julio Capote

This is common pattern in website navigation, where it highlights the link (usually by setting class=”active”) that took you to the current page while you are on that page.

First, define a helper:
def is_active?(page_name)
    "active" if params[:action] == page_name
  end

Then call it in your link_to’s in your layout as such:
link_to 'Home', '/', :class => is_active?("index")
link_to 'About', '/about', :class => is_active?("about")
link_to 'contact', '/contact', :class => is_active?("contact")

This effect is achieved due to how link_to handles being passed nil for its :class, so when is_active? returns nil (because its not the current page), link_to outputs nothing as its class (not class=”” as you might expect).#### 3813 views and 3 responses

- Jul  3 2011, 10:28 PMAndrés Mejía responded:You could also use the "current_page?" method instead of comparing against params[:action].

See:[http://apidock.com/rails/ActionView/Helpers/UrlHelper/current_page%3F](http://apidock.com/rails/ActionView/Helpers/UrlHelper/current_page%3F) 
- Dec 10 2011,  5:04 AMLadymur responded:I compare two methods. The variant in blog better for lage list, in apidock better if short mehu list, becouse it's dificalt to write controller and action eche time
- Mar 20 2012,  8:52 AMhoetmaaiers (Twitter) liked this post.

