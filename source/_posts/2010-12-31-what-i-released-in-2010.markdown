---
 layout: post
 title: "What I released in 2010"
 date: 2010-12-31 13:29
 comments: false
 categories:
 ---

 # Julio Capote
## This is an archived post
This is an archived post
[Previous](../../../posts/2010/02/post/390050440/on-google-buzz.html)  [Index](../../../index-2.html)  [Next](../../../posts/2011/01/post/2583891119/migrationfor-write-migrations-right-from-the-command.html) ### What I released in 2010
December 31 2010,  1:29 PM by Julio Capote

Here’s a recap of what I’ve worked on and released in 2010:

**Youtube Fraiche:**I couldn’t find a youtube downloader that worked on github, so I wrote my own one evening[https://github.com/capotej/youtube_fraiche](https://github.com/capotej/youtube_fraiche) 

**Uploadd and paperclip_uploadd:**I wanted to upload and store images off-site (using paperclip/rails) on an server which has cheaper bandwidth rates than S3. Using rainbows, this tiny rack script has handled over a 1.5 million uploads at a peak of 10-15 uploads/sec. Also, it’s been running for about 6 months now without a single crash. Thank you Eric Wong![https://github.com/capotej/uploadd](https://github.com/capotej/uploadd) There is also a plugin for the popular paperclip gem to use uploadd as a storage backend transparently.[https://github.com/capotej/paperclip_uploadd](https://github.com/capotej/paperclip_uploadd) 

**mrskinner:**Tiny javascript for making the site gutters clickable based on a fixed width layout:[https://github.com/capotej/mrskinner/blob/master/mrskinner.js](https://github.com/capotej/mrskinner/blob/master/mrskinner.js) 

**existential:**Completely inspired by Nick Kallen’s[post](http://pivotallabs.com/users/nick/blog/articles/272-access-control-permissions-in-rails) on authorization, I wanted to extract that pattern into a rails plugin that I could use for all my projects. I use devise/existential for all my projects now.[https://github.com/capotej/existential](https://github.com/capotej/existential) 

**has_opengraph:**Easy way to participate in opengraph and draw facebook like buttons. Just annotate your models with meta data, and draw it in your view easily.[https://github.com/capotej/has_opengraph](https://github.com/capotej/has_opengraph) 

**chewbacca:**I kinda feel bad that I took a cool name for such a lame script. Anyway it’s a set of rake tasks that provide a hair of abstraction above scp. Useful when you have a set of files locally that map to a different set of files remotely.[https://github.com/capotej/chewbacca](https://github.com/capotej/chewbacca) 

I already have tons of stuff in the works for 2011!#### 1086 views and 1 response

- Sep  5 2011,  5:51 AMalanbedford liked this post.

