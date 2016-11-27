---
layout: post
title:  "Setting Up Jekyll"
date:   2016-11-27 20:02:16 +1000
categories: jekyll
---
It took me way longer than I care to admit to setup this jekyll powered blog.

The main reason being is that I'm not so comfortable working from the Terminal yet, and using GEM, homebrew, etc are all still fairly foreign to me.

So when I was trying to follow the Jekyll installation instructions, I was getting an error saying that it couldn't download over https.

This sent me on a goose chase, but I was chasing the wrong goose.

What I actually needed to do, was update Ruby. Which I would've done sooner using rbenv, however I didn't realise that update-ruby was also out of date; meaning rbenv couldn't actually find the later versions of ruby.

Once ruby was updated, then I could update gem and everything worked a lot smoother.

I'm looking forward to styling my Jekyll blog over the next couple of weeks, and getting more familiar with it.
