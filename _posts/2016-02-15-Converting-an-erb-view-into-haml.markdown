---
title: Converting an erb view into haml
layout: post
date: 2016-02-15
---
## Writers Block
Let's be honest, I dislike writing. This was something that I hated as a scientist, really couldn't get over, and I recognized it was an integral part of my future career success. Ironically, now I'm pushing myself to write. I start with this because I made it a module goal to write one blog post every week for six weeks and we are starting week 3 and I have yet to push a full post out. I have started and stopped, written and deleted and re-written, and just not finished. I  have mused on different topics and realized that what I wanted to be a single blog post could easily be ten posts, and I didn't know how to split that up. So the result has been nothingness and today is course correction time.

The first week of Module 2 was building out a CRUD app in Sinatra. I attempted to push myself by choosing the spicy option and creating a [Robot World.](https://github.com/erinnachen/robot_world) I went down the HTML/CSS/Bootstrap hole, and I think it looks pretty good for a first attempt. An extension on this project was to convert our views from erb into haml. I didn't get a chance to do that last weekend, so here is a first attempt to porting views into haml. (Groundbreaking I know!)

## At the beginning
Where to start? Well, turns out that the simplest view is the root dashboard view

<img class= "image" src="/images/robot_intro.png">

The not-so-clean erb (actually just HTML!) looked like this:

<img class= "image" src="/images/dashboard_erb.png">

I'm basically nothing without google, so I did the monkey thing and found [this basic tutorial](http://haml.info/tutorial.html). Also, bold statement:

> Haml feels odd for the first 20 minutes, but then after that you will be faster.

Turns out haml is a gem ([erb](http://ruby-doc.org/stdlib-2.3.0/libdoc/erb/rdoc/ERB.html) is part of the Ruby standard library), so go and `gem install haml` and include it in your Gemfile. There's also a [http2haml](https://rubygems.org/gems/html2haml/versions/2.0.0) gem for those who are so inclined.

## Converting that erb(raw html) into haml
Here we go:
1. Take out those divs
2. No more crazy closing tags!
3. Indent your content (ala Python) to clearly nest elements in elements. (If you don't know this by now, I love indentation)
4. For those pesky tags, like anchor tags that have stuff you want to assign, throw them in a hash:

`<a class="btn btn-primary btn-lg" href="/robots" role="button">See pre-existing robots</a>`

becomes:

` %a{:class => "btn btn-primary btn-lg", :href => "/robots", :role => "button"} See pre-existing robots`

So here's the .haml file after the conversion:

<img class= "image" src="/images/layout_haml.png">

No syntax highlighting 😐, but the code looks cleaner.
However, I forgot one thing! Here's the page when it's displayed:

<img class= "image" src="/images/robot_intro_pre.png">

OH NO!!! What happened to my hours of styling? I forgot that `layout.erb` basically included all the pesky styling things, like my css! I know we all like 90's throwbacks, but you know... let's go and bring back those stylesheets.

So we need a file called `layout.haml` that will serve the same purpose of `layout.erb`. This is what `layout.erb` looked like:

<img class= "image" src="/images/layout_erb1.png">

And here is what happened to it after the haml-ification:

<img class= "image" src="/images/layout_haml2.png">

Some points that I will probably require some research:

I couldn't get the link tag to take in a hash. The attributes are wrapped in parens and look like what you would get in the html.

Supposedly haml doesn't like JavaScript. I have no idea if those Bootstrap tags at the bottom are working... but whatever.

Also the `aria-hidden="true"` that used to be part of my hearts. Not quite sure what that did, but visually doesn't look any different. It seemed to break when I tried to enclose it as a hash. Yeah...

## The conclusion?
Haml: I thought the lack of tagging would be cool, and indentation is a big sell. I'm thinking I may stay with erb for a little while longer to render my views. But maybe I'll just keep pushing through. Also I have to find some colors for haml in my text editor if I'm going to work with it regularly. Those fancy fancy colors.
