---
title: Cross-Origin Resource Sharing (CORS) and APIs
layout: post
---
### At the End: The Front-End
I've been at the Turing School for over 6 months now. We started in Module 1 buried in the depths of the stack, working with pure Ruby. I am basically a week from graduation and I have spent the last six weeks writing code primarily in JavaScript. So let's discuss something that one will not encounter until they have spent some time working on the front-end, Cross-Origin Resource Sharing(CORS). A disclaimer before I jump in, after wrestling with CORS in two projects, I'll say if you come across CORS, maybe you need to re-think your approach. I'll definitely address this at the end of this post.

To set the stage, here are descriptions of the two projects where I have encountered CORS. The first project was my personal project where I built a Rails application that would take in dog photos and send them to a second application built in Python that would classify the photo by dog breed. Sounds fun? It's still under construction, but you can find the Rails site [here](http://paws-app.herokuapp.com/). The second project was an 8-person team project that involved two applications, a front-end client built in JavaScript and React, and an application originally built-in Rails with a front-end and backend, but is slowly becoming solely a backend API.

Do you see the similarity between these two projects? If not, here's the "I'm tired, don't want to think" answer: A front-end application is utilizing JavaScript, likely AJAX, to make a HTTP request to **another** application for information of some kind.

### The Same Origin Policy
What is the problem with wanting to load information using AJAX? It's all the rage to have single-page apps, no one likes to wait for pages to load (I myself have a low tolerance for slow internet connections), and React makes these pages super, super responsive.

You may not know that your browser has a security measure in place called the same origin policy (I certainly had no idea...). If you are on a certain site and that site wants to initiate other requests to another site, say to fetch more information, your browser will not allow it to. Same origin is pretty strictly defined:

  * Same protocol: http and https **NOT** the same
  * Same hostname: www.twitter.com and api.twitter.com **NOT** the same
  * Connection port: localhost:3000 and localhost:4000 **NOT** the same

When I was trying to get my doggie breeds from my Python app, this was a cross-origin request. So Chrome blocked it (or tried to save me from myself...), and gave me this sweet error message.

```
XMLHttpRequest cannot load https://my-awesome-rails-api.com/api/v1/allthings.json. No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'http://my-sweet-react-client.com' is therefore not allowed access.
```

I was pretty unhappy. I'm not well-versed in security issues, so this statement from the [Mozilla docs](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) really didn't register with me: `The same-origin policy restricts how a document or script loaded from one origin can interact with a resource from another origin. It is a critical security mechanism for isolating potentially malicious documents.`

### Relaxing the same origin policy
The browser is trying to prevent you from receiving that sweet sweet API information that you wanted. Sad...or RAGE-inducing. How do you get around this? Perhaps the easiest way to enable cross-origin requests is Cross-Origin Resource Sharing(CORS). CORS is a standardized **handshake** process for friendly cross-origin requests. You can read about the nitty-gritty details [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS) or [here](https://www.w3.org/TR/cors/).

A question for you should now be, are you friendly with that backend API developer in the corner? Notice that I attempted to emphasize that CORS involves a handshake. The browser tends to take care of the front-end headers required for CORS, but it's also expecting headers in the response from the server. On the server side, the response must respond with a header with **Access-Control-Allow-Origin**. Turns out Rails does **NOT** do this by default. So pass that backend engineer a sweet Coors, and hope they enjoy puns!

### Cheers to you, backend engineer!
For me it was pretty straightforward to implement CORS protocol on the backend. Don't give me too much credit here, there are nice gems and libraries for it. In Rails, the [rack-cors](https://github.com/cyu/rack-cors) gem has a good README and some code [examples](https://github.com/cyu/rack-cors/tree/master/examples). Include the rack-cors gem in your Gemfile, and bundle. Add the following configuration into your application.rb file:

<img class= "image" src="/images/rack-cors-config.png">

For Python, two lines were added to my router, and it ended up looking like:

<img class= "image" src="/images/flask-cors-config.png">

### Final thoughts
If you were friendly with the backend engineer that is serving up that API, then you can have a CORS-enabled backend in no time. But what if that API is not controlled by you? There was something special about those AJAX calls that I was making. For both apps, the front end was making calls to an API without authorization tokens or keys. In addition, the front-end client I was working with was purely in development and since it was a static page it actually had no router in the project.

If there were keys, I probably would never have made a cross-origin request. In order to keep my API keys secured, I would have sent the AJAX request to an endpoint on my own app's backend to make the outgoing API request. For the app in development, this approach could also be relevant because some sort of backend server will be needed in production. That was my foray into the front-end, and I hope I'll return to the backend in the near future where Coors will be coming my way.
