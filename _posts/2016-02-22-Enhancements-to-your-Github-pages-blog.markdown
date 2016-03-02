---
title: Enhancements to your Github pages blog
layout: post
date: 2016-02-22
tags:
- jekyll
- enhancements
---
## It's all a work in progress
It is currently week 11 of 27 of my "stay" at the Turing School. I started this website because a personal website with a blog post was required as intermission work between Modules 1 and 2. You should already know that it took way too much time to style it (see [here](https://twitter.com/intheerinna/status/692337171848654848)), that [Bootstrap](http://getbootstrap.com/) would have really helped, and [Bootstrap Studio](https://bootstrapstudio.io/) made me cry over all the lost hours spent trying to figure out anything related to CSS.

I guess I have a blog, it's basically not ugly and functional, and I am moving forward. Styling aside, there were a few things that I wanted on the site (primarily seen [here](http://jmcglone.com/guides/github-pages/)) but did not really figure out before this site "had" to be live, and I am putting them in today. So how do you make your blog more awesome? Here we go:

## Enhancement 1: disqus so you can say amazing things about me
Comments are good things right? Well, it feels like a blog should be commentable. I went with [disqus](https://disqus.com/) as the service to enable comments because I have seen it all around and don't really know any better. It's pretty straightforward to signup, just choose a shortname that you are ok displaying on your site, since it says you can't change it...

I chose the universal code option and there are two basic steps, and two additional steps for post counts. Step 1 is to paste the code provided into your html, I put this in a `disqus.html` file and put it in my `_includes` folder, which also has my header and footer. I then had to include this html file through Liquid injection in my [layout/post.html](https://github.com/erinnachen/erinnachen.github.io/blob/master/_layouts/post.html) file. I put this towards the bottom because I assumed that is where I wanted comments.

Step 2 which is recommended, was a bit wonky to figure out. There are two lines in the universal code which say: `Replace PAGE_URL with your page's canonical URL variable` and `Replace PAGE_IDENTIFIER with your page's unique identifier variable`. These are supposed to be dynamic, and I'm not super familiar with extracting those variables in a Jekyll-served page. I stumbled upon something, so maybe it'll work:
{% raw %}
this.page.url = "{{ page.url }}";

this.page.identifier = "{{ page.title }}";
{% endraw %}


## Enhancement 2: analytics so I can figure out if I'm writing to myself
Clearly I'm not trying to make money off this blog, but it would be nice to know if anyone was stalking me, or just what traffic looked like. There are other data analytics pages out there, but until my blog takes off I am going to use Google analytics for now. I began by signing up for a [Google analytics account](https://www.google.com/analytics/).

I am one to try to "optimize" things even if I have no idea what I am doing or even if it doesn't really matter. It's a [millennial thing](https://www.netflix.com/title/80049714)(?) I was pretty skeptical when I saw this:

<img class= "image" src="/images/sign-up.png">
I went with it. I agreed to all the conditions, filled out some basic information, and I was informed to paste some JavaScript into all the pages I wanted to track. I then asked where should I put this JavaScript, and [the basic answer](http://stackoverflow.com/questions/6824095/best-place-to-insert-the-google-analytics-code) is it probably doesn't matter that much. (I ended up sticking it in the `<head>` tag.)

## Enhancement 3: that /blog/ path
This feature actually is not default when serving up your blog in Jekyll, which is what Github pages uses. That's just silliness. But it's a simple fix, just throw the line:

`permalink: /blog/:year/:month/:day/:title</center>`

in your `_config.yml` file and you too can have visit your posts at:  

http://username.github.io/__blog__/YYYY/MM/DD/name-of-your-post

instead of:

http://username.github.io/YYYY/MM/DD/name-of-your-post

Subtle difference, yes. Crazy about weird little things? That's me.

## Drinking from the firehose
In most of my endeavors, there are challenges to getting started. I am really trying to not get paralyzed by too much information and keeping the momentum going when I do get started. I don't know whether these enhancements will actually make blogging more fun in my mind, but we'll see. Maybe I should just think about moving to Wordpress...
