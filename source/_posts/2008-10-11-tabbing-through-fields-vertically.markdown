---
layout: post
title: "Tabbing through fields vertically"
date: 2008-10-11 01:54
comments: false
permalink: /post/54058512/tabbing-through-fields-vertically
categories:
---

 # Julio Capote
## This is an archived post
This is an archived post
[Previous](../../../posts/2008/09/post/52467447/why-mootools-or-why-not-jquery.html)  [Index](../../../index-2.html)  [Next](../../../posts/2008/10/post/54266325/arrow-key-navigation-for-text-fields.html) ### Tabbing through fields vertically
October 11 2008,  1:54 AM by Julio Capote

Sometimes it’s useful to switch the browser’s default tabbing behavior (left to right) to the opposite (top to bottom) when your input fields are in a grid layout instead the of the usual single column layout. Having to do this manually is a real pain, especially for large grids; So here is a solution in javascript, using mootools:
window.addEvent('domready', function(){
    var trs = $$('#mytable tr')
    var accum = 0
    trs.each(function(tr, trindex){
        accum = trindex + 1
        tr.getChildren().each(function(td, tdindex){
            td.getChildren('input')[0].tabIndex = accum
            accum = accum + trs.length
        })            
    })
})#### 259 views and 0 responses


