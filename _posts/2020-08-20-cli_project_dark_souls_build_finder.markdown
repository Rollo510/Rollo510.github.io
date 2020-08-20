---
layout: post
title:      "CLI Project: Dark Souls Build Finder"
date:       2020-08-20 04:06:20 +0000
permalink:  cli_project_dark_souls_build_finder
---


It's been over an hour since the last bonfire.  I've been tempting fate by pushing on, but I know I'm likely to find a shortcut back to safety soon.  Every enemy encounter depletes charge after charge of my life-giving Estus Flask.  If I die now, I'll have to fight my way back through the darkness of the Abyss to where my corpse lay.  Die again without reaching it, and I lose everything I worked for--an hour's worth of grinding currency.  It'll be like this past hour meant nothing.  This is the Dark Souls way: extreme difficulty that rewards you for taking chances and keeping calm in increasingly dire circumstances.  Although I say I would lose everything, that isn't necessarily true; Dark Souls is a video game that, like coding, builds upon itself the more time you spend with it.  While you might lose currency and items when you die, what you can never lose is knowledge.  Now, you know where the enemy is hiding, you know what traps await, and you can equip gear resistant to the effects ahead.  Neither Dark Souls nor coding is easy--that's for sure-- but both reward you for investing your time in them. 

The idea of my CLI Project was to provide an interface that would ask you for a weapon type, and then provide a list of weapons matching that type, allowing you to select one to learn more information about it: Strength requirements, Dexterity requirements, and so on.  Finding an API was relatively easy; I searched for Dark Souls 3 APIs and found the first one to be pretty straightforward; however, there was one major problem that blocked my progress (in true Dark Souls fashion).  The API listed every weapon in the game, but everything was stored in one hash, and the second-highest level of the hash was an "ID" value that was totally arbitrary.

```
                      {
                             "count": 206744,
                             "ds3_builds": {
                                       "408521": {
																			 ...
											]								 
```

Essentially, the ID "408521" was preventing me from accessing the key-value pairs further in the hash.  I eventually managed to come up with a solution that involved chaining .collect, .find, and .each methods to keep diving deeper into the hash like some sort of janky Matrix / Inception hybrid.  While this ended up returning the hash items that I wanted, it desperately needed to be refactored because my "Weapon" class somehow ended up with the responsibility of "putting" the text displayed within the interface.  Like trying to use a Shield as a weapon, it definitely didn't work well.

One of the best parts of Dark Souls is the ability to cooperate with friends online to tackle bosses that you can't beat on your own.  In similar fashion, I had to ask for help to fix the broken code I'd made.  After a little bit of brainstorming, my mentor, Juan, and I found a way to make my code accomplish the same general purpose as before, but with better functionality and eloquence.  The ID issue above was solved by using .each to iterate over a mapped "results" hash, then setting a local variable to each of the attribute requirements (Strength_req, for example), and finally creating a .new object of the Weapon class with arguments of each of those attributes.

The best things in life are those that you've worked for.  Nothing worth doing comes easily.  Dark Souls is a game that embodies these principles.  Maybe that's why it's one of my favorite series of all time-- and also why I enjoy coding so much.  I like the feeling of accomplishment that comes from pushing through uncertain circumstances and being rewarded for doing so.  Completing this CLI was challenging, sure, but it also taught me how to approach a project from scratch.  I've made it to the next bonfire, spent my currency to level up, and am ready to tackle whatever comes next.








Also, wow, I'm sorry about how cheesy I made this whole blog post, this really isn't my personality at all, I live for the punishing difficulty and I would never accept help in Dark Souls because the whole point is to "git gud" or die.  Also, if you're reading this and have any idea what I'm talking about:
Bloodborne > Dark Souls > Sekiro > Dark Souls 3 > Demon's Souls > Dark Souls 2.



