---
layout: post
title:      "Manage your Stock portfolio with Stockey!  Sinatra Final Project"
date:       2020-09-18 02:07:20 +0000
permalink:  manage_your_stock_portfolio_with_stockey_sinatra_final_project
---


The idea for Stockey came to me as I sat thinking of a way to store all of my current stock investments in one place.  I had a dream for this project to turn into a social-media platform for users to discuss their stock and options trading; however, I quickly realized I didn't have the know-how to execute something so broad and challenging with only a week of training in Sinatra.  So instead of giving up, I decided to lay down the groundwork in the hopes of being able to update it fully later on when I have much more experience constructing websites.  Thus, Stockey was born: a website that allows a user to add their stock portfolio and manage their prices.  

In all honesty, the most difficult part of building Stockey was deciding what it was going to do.  There's infinite possibilities, but they don't all necessarily make sense.  Should users be able to edit stocks that they don't own?  What attributes should each stock have that reflect the most vital information?  Can I even do this?  The answer to that last one is still up in the air, but I feel confident that I've created something that at least *feels* like a legitimate website.  Fundamentally, I understand how models, views, and controllers work, but getting everything to fall into place is a whole other beast entirely.  

The most challenging part of making a website is making sure that each model, view, and controller knows who it's talking to and what it wants to achieve.  In particular, building out Edit functionality seems simple in theory, but in practice, bootlegging the code so that you can properly update an object is tougher than it seems.  Take, for example, the code below:

```
<form action='/owned_stocks/<%= @owned_stock.id %>' method='post'>
<input id='hidden' type='hidden' name='_method' value='PATCH'>
```

The owned_stock in this instance is essentially a representation of the JOIN table that connects a User to a Stock.  In order to edit the stock, do I need to edit the owned_stock object, or the actual stock itself?  Will editing the actual stock lead to bugs for other users?  Well, turns out it's both.  Because of the association between a User and a Stock, it's necessary to produce methods that assign a current_user to the stock, allowing only that person to make changes to it.  This is where the social element that I had in mind comes into play: I wanted everyone to be able to leave comments, make changes, and suggest sell / buy prices for a stock that they all collectively own.  Of course, this is a classic example of biting off more than I can chew, however, I at least have the foundation to build this functionality in later.

If there's a major takeaway from this project, it's that websites are **substantially** harder to build than they look.  While we think "oh I'll just put in Facebook.com and it'll take me to the site", under the hood there are models creating new objects, views displaying the pages, and controllers telling everyone what to do.  Fundamentally, it all makes sense to me; bouncing around from one URL to the next, displaying its contents, and allowing the user to decide what to do next are all so simple to understand.  But there comes a point where that stock name *just wont display* and it becomes a stuggle.  Despite all of this, understanding how websites work is a major intellectual leap that really makes you wonder at the complexity of technology that we have taken for granted.  And while I did struggle a bit creating something that I could actually be proud of, here I am.  So maybe the next time you hear the name Stockey, it'll be the talk of Wall Street (doubtful), and you'll remember reading this and remember the poor soul that struggled in vain for days to make something that might actually have some use... or maybe you won't.  Stocks *are*  pretty confusing, aren't they?



