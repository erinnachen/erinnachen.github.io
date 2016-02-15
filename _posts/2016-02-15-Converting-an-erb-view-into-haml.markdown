---
title: Converting an erb view into haml
layout: post
date: 2016-02-15
---
## Writers Block
Let's be honest, I dislike writing. This was something that I hated as a scientist, really couldn't get over, and I recognized it was an integral part of my future career success. Ironically, now I'm pushing myself to write. I start with this because I made it a module goal to write one blog post every week for six weeks and we are starting week 3 and I have yet to push a full post out. I have started and stopped, written and deleted and re-written, and just not finished. I  have mused on different topics and realized that what I wanted to be a single blog post could easily be ten posts, and I didn't know how to split that up. So the result has been nothingness and today is course correction time.

The first week of Module 2 was building out a CRUD app in Sinatra. I attempted to push myself by choosing the spicy option and creating a [Robot World.](https://github.com/erinnachen/robot_world) I went down the HTML/CSS/Bootstrap hole, and I think it looks pretty good for a first attempt. An extension on this project was to convert our views from erb into haml. I didn't get a chance to do that last weekend, so here is a first attempt to porting views into haml. (Groundbreaking I know!)

## At the beginning
Where to start? Well, turns out that the simplest view is the root dashboard view:

<img src="/images/robot_intro.png" alt="robot dashboard" class = "image" />

The not-so-clean erb (look at those white spaces!) looked like this:

<img src="/images/dashboard_erb.png" alt="dashboard erb code" class = "image" />

I'm basically nothing without google, so I did the monkey thing and found [this basic tutorial](http://haml.info/tutorial.html). Turns out haml is a gem, so go and `gem install haml` and include it in your Gemfile. There's also a [http2haml gem](https://rubygems.org/gems/html2haml/versions/2.0.0) for those who are so inclined.

## It took way longer to write this post than to convert erb into haml
