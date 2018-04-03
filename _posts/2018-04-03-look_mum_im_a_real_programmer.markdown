---
layout: post
title:      "Look mum, I'm a real programmer!"
date:       2018-04-03 05:52:49 -0400
permalink:  look_mum_im_a_real_programmer
---


![](https://i.imgur.com/kyizZZu.png)
# I just made my final commit...
...(until code review, I suppose...) on my first ever Portfolio Project. A fully functioning piece of code which a user can interact with, make decisions, find the latest bang-up-to-date information from a website and - of particular interest to me on a personal level - access this super quick, easy and free. *[Kind of. It helps if your user is not scared of Terminal or command line interfaces in general]*

<img src="https://i.imgur.com/99V7226.gif" alt="ginger matrix" width="100%">
# It's been quite the journey
I've been excited about this project for a while now. I was having a great time learning everything taught thus far on the Flaitron Learn-co curriculum but let's face it, knowing that you're soon going to be making a whole working program and * **publishing it**(!!) * really helps you push through the tougher labs! 

So when the day arrived and it was time to get going on my own project, whatever I wanted, I excitedly started with...

## Ideation
<img src="https://i.imgur.com/qioSpcd.gif" alt="Dynamic html" height= "250" height= "100" align= "right">
I quickly found an idea. I move a lot and frequently find myself skulking around scanning for any WiFi hotspots. There used to be a great website for this but now they've mostly disappeared and been turned exclusively into mobile apps. That's great and all but I thought it would be pretty great to have a simple CLI with which you could search for your location and have it return all the local hotspots along with detais on address, restrictions, maybe even a password or two! So I found two websites that still do this. One of them, [WiFi Spc](https://wifispc.com/) is pretty nice but a bit too fancy for my scraping ability thanks to the dynamically updated html *(see right)*

The other, [WiFi Free Spot](http://www.wififreespot.com/) was looking a likely candidate until I tried to actually parse what I was scraping and discovered that whoever designed this website was allergic to class and id tags. I set out to do my best attempt at gracefully navigating the endless, anonymous `<p>`s but eventually realised that it was futile and started a period of wondering what to make.

Every idea I came up with had either already been implemented in a gem or was useless. I like seemingly 'useless' things sometimes but I didn't feel like that approach was quite right for this project.

I settled on making a news and information scraping app for [Berklee Valencia](https://valencia.berklee.edu/) which is where I did my Masters courses. It was during my Tech & Innovation Masters that I was first introduced to code and logic so it seemed apt that I make them a little something in return. **Idea** in hand I set out to plan.

I thought I planned pretty well. Turns out I didn't, more on that later.

And so now with (what-I-thought-was) a great **plan** in hand, I set out to write my code
<br><br>

I quickly found that I was going to require a few...
## Crash courses
### Local environments
So I actually spent my first official day on this project setting up my local environment. I had been keen to get my local environment setup for a while but didn't feel qualified. It seemed suitable though - my project, my code, my environment - and I decided that day was to be the day. 

And by 'the day' I mean literally the whole day. 

It wasn't hard but it was a lot of staring at downloads which were long enough to make you twiddle your fingers but not long enough to go and make a hot chocolate, you know? As part of this I got a specific extra crash course in [rvm](https://rvm.io/) which I have since touted to all my friends. It allows you run various Ruby versions and easily switch between them, all whilst leaving alone the Apple-proprietery-flavour of Ruby to sulk in the corner where it hides becasue it doesn't like change.

I'm so happy to have my own environment setup now. It does feel like upgrading from an intermediate to a professional musical instrument.

### git and Github
- I set up this repo 4 times because I kept making little mistakes and wasn't 100% sure how to fix them without just deleting the whole thing and starting again. I do however feel very confident in this now as a result! 

- I used branches (not really as much as I had hoped since there are a few commits on the master branch which are broken versions) which was something I was unsure about before. 

- git and GH confidence levels have soared. It does all come a lot more obvious when you are working on a complete project. You suddenly realise exactly why version control is a Pretty Great Idea.

### Building a Gem and publishing to RubyGems
This was a 'fun' labyrinth within the world of requires, require_relatives and gemspecs. I could write a short novel documenting all the variations I tried before I finally got the magic combination of requirements. 
*Hmm.. I wonder if the Room of Requirements at Hogwarts would be useful for this... *

<img src="http://78.media.tumblr.com/8ff59cc1d79df24e9fada09577fbde0b/tumblr_ntbt2uaEPq1qbajilo2_500.gif" alt="room of requirements" width="100%">

*huh, what, sorry? I'm back now...*

- I ended up looking at the [worlds-best-restaurants](https://github.com/cjbrock/worlds-best-restaurants-cli-gem/) source code and attempting to apply it to mine to resolve my file requirement and gemspec woes. It was still a long frustrating learning process but I did eventually get it.


- [bundler](http://bundler.io/) was great to kick off the whole project as it created a familiar looking structure to get going in. However, when it came to publishing, I ended up rewriting their provided gemspec and using the simpler structure suggested by [RubyGems](http://guides.rubygems.org/).  The RubyGems guides are a great resource and I will be getting deeper into it when I make another gem.
<br>


## What I thought I had done:
- I gave it what I initially believed was a great, planned out, structure, I was proud and felt like I had thought it through well
- I did eveything step by step, was very careful with my commits.

## What I actually did:
-  In retrospect I think maybe I didn't have enough sleep the day I did my planning or something because the **structure**, whilst I did make it work, was not graceful. As I was about to publish the gem I read through everything and realised that I could have made everything cleaner. As I kept looking and started finding things that could be improved such as:
* **Load times** I had the program re-scrape everything everytime there was a menu switch. Madness. I did have a theory behind it at the time but in practice it was pretty silly.

* **Responsibilities** Avi Flombaum is often bringing up distribution of responsibilities and I had it in mind the whole time planning, designing and writing my program. But when I came to review it myself, I realised that actually I had inconsistencies and it was bugging me. The way I had chosen to approach it, I believe would be termed as an [anti-pattern](https://en.wikipedia.org/wiki/Anti-pattern), which is not nearly as exciting as anti-matter.

* **Commiting** As the project came on and I started to move more quickly, it was easy to get swept away and forget to commit for a bit too long.

##  So I refactored...
* **Load times** I made adjustments so that it didn't scape every time. What was I thinking before!? I had the option of either just moving a few lines of code or making a few small if statements. I went for the small if statements as it let me maintain the logic and distro of responsibilities concept which made me put those lines of code in those places originally. 
Result? Much less time waiting around! Thanks to my choice to use if statements, I also managed to not lengthen my initial load time. I'm scraping quite a bit of info and doing it all when launching the program didn't seem the best idea especially as most users will not choose to read every single article and program. 

* As for  **responsibilities**, I don't know why I didn't originally have a Category class. I mean, it works without it but in retrospect, it's not graceful at all. In my original iteration I also had my Article and Program classes working only with class methods which again, in retrospect, is absolutely ridiculous! So I made adjustments to those and added the Category class and suddenly everything looked a lot cleaner. As such making the consequential adjustments to any affected methods was quick and easy.

* **Other refactors** I made a couple of other adjustments to keep the app as [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) as possible. I had done pretty well in my first version except for whereever I checked input I was checking for incorrect input and 'goodbye' type statements separately each time.

*So where I had something like...*
``` 
if input.to_i.between?(1,category.articles.length)
      show_article(category, input)
    elsif input == "menu"
      programs_or_news
    elsif input.match(/hasta luego|exit|bye|ciao/)
      goodbye
    else
      say_what
    end
	```


*I replaced it with... *

```
if input.to_i.between?(1,category.articles.length)
      show_article(category, input)
    elsif input == "menu"
      programs_or_news
    else
      if_not_that_then_this(input)
    end
	```
	
*and then I added this method:*
	
```
def if_not_that_then_this(input)
    if input.match(/hasta luego|exit|bye|ciao/)
      goodbye
    else
      say_what
    end
  end
	```
	
It doesn't look like much of a change but I had written out the code in `if_not_that_then_this` 4 separate times in total. Wrapping it into it's own method does look a lot neater.
	
Another example of a small syntax thing I changed was the decision of whether to keep this line:
*  `elsif input == "1" || input == "2"`

or adjust it to
*  `input.to_i.between?(1,2)`

I went with the between? option in the end since I have that method used consistently elsewhere in the program in situations where the parameters are dynamic. 
eg: `if input.to_i.between?(1,category.articles.length)`

Even though I know that in the foreseeable future, that 1,2 parameter is very unlikely to need to change, I figured I might as well make it easier for myself if it ever does. A tiny point but I think it's a good thing to be thinking about.

## What I will do differently next time:
- I will write a test suite. **Before** writing my code! I I think I will add tests retrospecively to the berklee-valencia gem as an exercise in writing my own tests and also to make my gem more credible.
- Following up from that point, I will not rush in so hard. I really thought I went in with a solid plan but now experience has taught me that it is worth giving it a bit more time before starting to write code.
- The whole process will be smoother as  hopefully I won't be re-learning git, bundler and rubygems next time! As  did the refactor I also noticed that I was getting a lot quicker at tracing bugs and sometimes seeing errors before they happened. As with any skill I am sure this will keep improving with time and hopefully the face-plant count will decrease with each new project.


## New directions (and dependencies)
I had a good time poking around [RubyGems](http://) to see what's out there already both whilst deciding what to make and later when I had got more comfortable with running other cli apps and was checking some out. 
I wasn't planning on using any extra gem dependencies in my project but I came to an impasse when I was thrown this delightful error:
```
/Users/Gingertonic1/.rvm/rubies/ruby-2.4.1/lib/ruby/2.4.0/open-uri.rb:225:in `open_loop': redirection forbidden: https://valencia.berklee.edu/academic-programs/summer-programs/three-week-valencia-summer-performance-program/ -> http://valencia.berklee.edu/academic-programs/summer-programs/spain-summer-performance-program/ (RuntimeError)
	from /Users/Gingertonic1/.rvm/rubies/ruby-2.4.1/lib/ruby/2.4.0/open-uri.rb:151:in `open_uri'
```

Something was going wrong on this line of code:
`program = Nokogiri::HTML(open(url))`

The url I was passing to [nokogiri](http://) via [open-uri](http://) was being redirected and apprently that's not something than [open-uri](http://) can deal with by itself. After a short poke around on [StackOverflow](http://) I found out about a gem called
[open-uri-redirections](http://) which does exactly what it says on the tin. I soon had it in my gemspec, adjusted that line of code to read:
`program = Nokogiri::HTML(open(url, :allow_redirections => :all))`
and suddenly everything was good again.


## Posterity
- I documented most of the process using [Silverback](https://silverbackapp.com/) screen and webcam capture software. My face when I finally successfully published, downloaded and ran my own gem is fairly self-explanatory *(see Exhibit A, right)*

<iframe width="100%" src="https://www.youtube.com/embed/QHVPQejfOX0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
<br><br><br>

- *(I also managed to capture a few good 'I give up' faceplants onto my bed during the process which I will refrain from sharing.) *


## Grab a friend
I am not exactly surrounded by coders. I am studying remotely and currently based in Adelaide, Australia but I move at least every 4 months for work. The last couple of years I've been moving every day during the summer and every 1-2 weeks in the winter (I was touring with the circus). Whilst this lifestyle is many varieties of fabulous, it's not quite so good for having the same people physically around you to consistently be sounding boards and give advice. I have been lucky to have had two particular 'phone-a-friend' gifts during this project:

1. My best friend from school, [Fahran](https://fahran.net/) is a tour de force of awesomeness. Her career trajectory towards being an astronaut was adjusted when she found coding and now the poor thing is on a train looking over this, my first ever real code project. It's all about balance in the universe - my background is as a professional musican and the more coding I do the musical Fahran seems to get. Amazing. 

2. Your friend doesn't have to be a coding genius however. Yesterday I was on a car journey with my wonderful housemate Sally who is a landscape architect and visual artist. I was trying to figure something out in my head for my refactor and I was hitting dead ends. I then announced I would be talking it through out loud, thus started, and suddenly within 2 outloud sentences, I had figured it out. 

It might be better if you don't tell your friend that they are standing in for a rubber duck.

# Improvements and next steps on this project?
I will very shortly be submitting my code for assessment and review. I'm quite proud of it but at the same time this will be the first time that I've ever had a sensible conversation with someone about code outside of tech coach screenshares. I am primarily very excited about it as I am fully aware that these kind of discussions and reviews are a major part of the life of a professonal coder.

Just last November I knew next to nothing and now I'm submitting a real working Thing. I only hope that my next steps continue to propel me along the way!

# How to keep these skills in shape?
I believe that's going to happen automatically through the upcoming projects. Having said that, I did have a couple of ideas for other cli scraper apps that came to me after I'd already started coding this one. It would be fun and helpful for skill maintenene to implement them at some point.

### 1. h2g2 / dontpanic / theguide
I can't believe no-one has made this ruby gem yet! I'd like it to scrape the [h2g2](https://h2g2.com/) website (The Hitchhiker's Guide to the Galaxy: Earth Edition). First version to retrieve the featured articles and the fully featured version to eventually be able to provide graceful access all the articles through CLI.

### 2. a visualiser of some interesting social or enviromental data
Generating something pretty and/or interesting (not an explicit visualisation but an artistic interpretation) based on something like... current oxygen levels or current uv index?

I'm so excited to keep learning with Flatiron continue adding skills together to make increasingly awesome things! I am starting to get a decent little library of ideas for future projects and any I don't make during the course, I can save for a rainy day after I've graduated!

# Here the beautiful location I was working at when finishing up the project.
Exquisite surroundings make everything much easier!

<img src="https://i.imgur.com/D0XHgJ7.jpg" alt="Encounter Bay" width="100%">














