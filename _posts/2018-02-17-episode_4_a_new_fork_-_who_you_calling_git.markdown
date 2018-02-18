---
layout: post
title:      "Episode 4 A New Fork - Who you calling Git?"
date:       2018-02-17 03:14:58 -0500
permalink:  episode_4_a_new_fork_-_who_you_calling_git
---


This is Episode 4: A New Fork, my 2nd blog post. And you thought the Star Wars canon was odd.


## New dialects
The land of Code has it's own particular dialect of the English language with plenty of words and phrases that I hadn't come across before, or at least not in the way they're used in my new method of communication.
Let's have a brief extract from my never-to-be-published tome:

##### The Programmer > Non-Programmer English Dictionary *[an extract]*:
***=***  `=` is an "assignment operator" which gives meaning to otherwise random words that the computer doesn't yet know. We can teach it the meaning of new words eg: `gingertonic = "total genius!"`. Now everytime I type in `gingertonic` and hit enter, it will respond with "total genius!" which is a demonstration that computers will believe anything if it's wrapped in quotation marks (`" "`)

***==*** 
If I try and say `2 + 2 = 4` and hit enter, it throws a fit: `SyntaxError: (irb):1: syntax error, unexpected '=', expecting end-of-input 2 + 2 = 4`

`2 + 2 == 4` however, gives a much more dignified response of `true`. 

In summary: `"=" != "==" && "=" != "===" && gingertonic == "total genius!"` but that's a story for another day.

***===***  you don't even want to know right now

***binding*** If you are working in one language or library, you can 'bind' another one onto it to get some extra functionality. In Ruby, we are often trying things out in IRB (Interactive Ruby) (see *REPL*) but sometimes we want to use Pry (see *pry*) to look in further. We don't have to leave IRB to do that, we can grab a rope and drag Pry screaming and kicking down to IRB-land and bind him on tightly with the rope, not so hard that he can't do his job but tight enough that when we should his name, he comes running over quick to see what the problem is.
The rope is metaphoric, please don't lash anything or anyone with a rope to your computer.

***clone*** What you usually get after forking. For more info read below (see *fork*)

***CRUD*** A cruddy acronym for 'Create, Read, Update, Delete' which describes some things that we do lots of everyday. Especially if you are on Facebook: Create a post, Read the post, (find a typo) Update it, (get poster's remorse), Delete it. 

***debugging*** I love the story of this word. One of the top BABs in programming, [Grace Hopper](https://en.wikipedia.org/wiki/Grace_Hopper ) in 1945 found a bug (a moth to be precise) in one of the tube relays of a massive fancy calculator made at Harvard. Indeed, the word 'bug' was used before this, as Thomas Edison mentions in a letter dated 1876...
> 'Bugs' -- as such little faults and difficulties are called -- show themselves and months of intense watching, study and labor are requisite before commercial success or failure is certainly reached.

... so whilst Grace didn't spark the invention of the word 'debugging', her experience certainly gave us a great story!

***DOM*** Not what you think. It stands for Document Object Model. And no, there's not a SUB. Not that I know of anyway....

***elsif*** A small bird who vocally responds only if the `if` bird says 'no!' If the `elsif` also says 'no!' then a team of other elsifs may come along to help out. If all the elsifs say 'no' then the wise `else` comes and decides for everyone.

***environment*** Much like our natural environment on Earth and beyond, we should strive to maintain the environment we keep for our code to live in and develop. If it's a clean, tidy environment, everything is more efficient, healthier and nicer to be around!

***fork*** Forking leads to Cloning. Forking is also what you do when you find some code in a repository (see *repository*) that takes your fancy and you decide to get a fresh copy of it. You can either play around with the fork itself or if you want, you can clone it down to your own computer and continue working on it.

***gem*** My friend Gemma who has a [bloggywog](https://howtoloseapenguin.wordpress.com/author/howtoloseapenguin/). 
Gems are also little packages of code which programmers make and give each other to make everyone's lives easier. These are specific to the Ruby language and there's a giant list of them over at [RubyGems](https://rubygems.org//).

***Git*** Git is, contrary to what you might think, a Good Thing. It can be a bit of a hassle and confusing at first so the name is possibly deserved at times, but it's worth it. Git is a tool which let's us keep all the code for one project in a filing cabinet system of our own design. We can easily create new cabinets out of thin air with a fresh copy of our main cabinet so we can experiement. What's really cool is that we can keep working on our new ideas in a quarentined area. In the case that our experiments blow everything up, everything is OKAY, becasue all the other cabinets are completely bombproof.
Once everything is working, everyone has been released from hospital and the problems are fixed, if we want to make the new (now safe) feature a part of our main project, git will do that for us seamlessly with only 1 or 2 lines of admin paperwork needed from us.

***GitHub*** Git byself can be used on our computer, disconnected from the world. GitHub is a handy way to keep a copy of everything online and if you like, other people are see it, fork it (see *fork*) (make a fresh copy), clone it (see *clone*) to their own computer and work on it. This is super useful in pair programming! (see *pair programming*)
There are other places that let you do this, [GitHub](https://github.com/) is just a super popular one.

***iteration*** (not be confused with looping) Go back to top of dictionary and for each entry, read its' name. If the entry name is *looping* then read the whole entry. 

***looping*** (not to be confused with iteration) (see *iteration*)

***nesting*** Things acting like Russian dolls.

***pair programming*** A super cool way to work, where two people work on the same code at once. One person is the 'driver' and the other is the 'navigator'. The navigator tells the driver what to do and the driver does it. If the navigator gets stuck then switch roles! You might be physically in the same room at the same computer in which case you just take turns on the keyboard but you can also use the magic of git to shove code back and forth.

***pry*** A sneaky way to stop time and look further into a problem. Basically turns you into Quicksilver from X-Men. (see *binding*)

***REPL*** Another cheeky acronym which I forget frequently. It stands for Read, Evaluate, Print, Loop. A REPL essentialy is a safe space to play and experiment with code. Impromptu REPLs for lots of languages can be created from thin air for your pleasure at [repl.it](https://repl.it/). 

***repository*** A place for storing things. Like code. Or hummus. Or mushrooms. A good hummus repository would be a cool, dark cupboard. A good code repository would be somewhere like [GitHub](https://github.com/gingertonic). A good mushroom repository would be the bin.

***SSH*** it's a trap. Secure Socket Shell. Designed to make your things safe, but your life hell. (Your milage may differ)

***string*** 
Let's ask Ruby the perennial question: 
`How long is a piece of string?`
It get's a bit pissy and goes off on one since it doesn't know so we give it a poke in the ribs and tell it that
`string = "twice as long as half it's length!"`
Now we reckon Ruby knows the joke, we ask again, this time in Ruby-speak:
`string.length`?
and it says 
`33`.
Long story short, Ruby doesn't get jokes. Nor do any other languages AFAIK. *sigh*


***Tic Tac Toe*** an enjoyable game for everyone except the programmer. NB for fellow Brits, this is the same as Noughts & Crosses.

## Remember, if in doubt, Google it!
![](http://www.articlesweb.org/blog/wp-content/uploads/2011/06/dictionary-google.jpg)















