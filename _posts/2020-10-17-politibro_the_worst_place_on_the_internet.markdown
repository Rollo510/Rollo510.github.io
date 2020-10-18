---
layout: post
title:      "POLITIBRO : The Worst Place on the Internet!"
date:       2020-10-18 01:22:09 +0000
permalink:  politibro_the_worst_place_on_the_internet
---

First off, let's get the introductions out of the way.  Politibro is a website that I created using Rails and a handful of CSS, yet still looks like a complete mess.  In case the meme-y nature of the name Politibro wasn't enough of a clue, this website was designed to be a forum for posting terrible memes and starting Internet fights.  The idea came to me after watching the first Presidential Debate, oddly enough (that's sarcasm).  Politics in America are a complete mess, everyone is yelling at each other, and there's no respect for one another's opinions anymore.  So what better way to embrace being American than by creating a website where you can yell at other users, post your own terrible memes, and just be an awful person?

To be fair, even though I've spent that whole last paragraph insulting my own project, I am pretty proud of how it turned out.  It's got all the functionality that you'd expect, including editing, deleting, commenting, etc.  Overall, the style isn't too bad either, if a bit bare-bones.  The real difficulty getting Politibro up and running came from incorporating nested routes into my controllers and views.  For whatever reason, I decided to use Comments as the Join linking together Users and Memes.  This ended up making the routes a bit shakey, but thankfully, that also perfectly embodies the spirit of Politibro.  I wanted the root page to be the Memes index as opposed to something related to a User because the idea is for all of the memes to be visible to all users, kind of like what you'd expect from a site like Imgur or Reddit.  

Further expanding on my troubles with nested routes, I struggled with the idea that when I wanted to create a new Meme or Comment, I had to nest both the model and the attribute in order to successfully create the object.  For example:

```
def create
        if params[:meme_id]
            @comment = @meme.comments.build(content: params[:comment][:content], user_id: current_user.id)
					etc.
						
```

Because I had spent so much time with Sinatra for my last project, I didn't understand why I needed to nest the [:comment] before the [:content] if I was getting that information from the form being sent.  The reason why is because the params hash that the controller action receives has not only information about [:comment], but info about [:meme] as well!  The controller is smart enough to build a comment out of the hash of info I sent it, but it needs to know what object to associate it to, thus, I needed to have an instance variable defined for the meme that the new comment would be associated with:

```
 def set_comment_meme
        @meme = Meme.find_by(id: params[:meme_id])
    end
```

Aside from struggling a bit with nested hashes and routes, the other major challenge of building Politibro actually wasn't even a project requirement at all!  I wanted Politibro to look clean and organized from the outside as a sort of representation of how the government appears to a lot of people.  When you see the Log In screen, you think, "Oh, this isn't so bad!" and then once you start looking at memes and seeing people comments, you suddenly realize, "Wow, this is actually terrible."  In order to achieve this effect, I used card-decks from Bootstrap for the Meme Index page.  Card decks size images into similar blocks, and also give you space for a small description.  This way, my memes are all uniform, despite being completely different sizes from whichever source they come from.  After spending hours tweeking it little-by-little, I came around to this CSS styling: 

```
.card-deck {
    margin-top: 20px;
    margin-left: 20px;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    grid-gap: 2.2rem;

```

This would allow for 4 cards per row, and give enough space for each image to actually be legible without being over-stretched.  

Now that I've completed Politibro, I can honestly say I'm impressed with how it turned out.  I really didn't think I had it in me to create something that actually feels and functions like a professional website, yet somehow I did.  I think that despite whatever else happens in my software engineering career, I know that I am at least proud of this one thing that I've made, and who knows, maybe someday Politibro will become the new Facebook.  


Then again, let's hope it doesn't, actually.




