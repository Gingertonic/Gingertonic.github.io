---
layout: post
title:      "Diving with Sinatra"
date:       2018-05-27 13:49:31 -0400
permalink:  diving_with_sinatra
---

<img src="https://i.imgur.com/CPXm1wk.gif" alt="menu fish gif" width="100%">


## Welcome to the [GROTTO](https://github.com/gingertonic/grotto)!

<img src="https://i.imgur.com/1iRgTqR.png" alt="Welcome to the Grotto.." width="100%">

So here it is. My First. Ever. Webapp.

## A what now?

Grotto is a dive log for SCUBA divers. I love diving and recently I loved it even more because my mystery engagement journey from 50ft undersea to 1700ft above sea started in a magical underwater cave whilst diving. It was only natural that I dedicate my first web app to my engagement. Right? That's normal, no?

## What's it made from?
<img src="https://media.giphy.com/media/11eR34PSlkrPTq/giphy.gif" alt="Lego" height= "350" align= "right">
From back to front we have:
* [SQL](https://www.w3schools.com/sql/sql_intro.asp)
* [ActiveRecord ](http://guides.rubyonrails.org/active_record_basics.html)
(with a cameo from [ActiveSupport](https://rubygems.org/gems/activesupport/versions/5.0.1))
* [Ruby](https://www.ruby-lang.org/en/)
* [Sinatra](http://sinatrarb.com/)
* [ERB](https://ruby-doc.org/stdlib-2.5.1/libdoc/erb/rdoc/ERB.html)
* [HTML](https://www.w3schools.com/html/html_intro.asp)
* [CSS](https://www.w3schools.com/css/css_intro.asp)

I also used [RSpec](http://rspec.info/) and [Capybara](https://github.com/teamcapybara/capybara) to write tests.

## Tests?
Yes! I am extremely happy that this project gave me the perfect excuse to learn how to actually write my own tests. In fact, before I even started coding the app, I made myself learn rspec/cabybara and then write the initial tests. At first it felt like I was writing code to test the tests. It took me the best part of two days to get it down. But once I had it figured out, writing the actuall app really did feel more like solving a neatly put together instruction sheet rather than stabbing in the dark and getting distracted by other things. Once my code outgrew my tests I added more tests and so on.

## Problems?
Yes. I will cover my top three favourites... (as it was not required of the project, I won't include CSS but oh boy, do I want to.)

### Gold medal goes to this piece of banter from ActiveRecord
`NameError: uninitialized constant User::Dife`

Yes, that says Dife. What is it? This is ActiveRecord's usually very useful and intelligent singularization/pluralization algorithm telling me that the singular of `Dives` is, of course, `Dife`.

Wow.

I mean, really guys,

I thankfully guessed pretty quick that it was a singularization issue and was able to move swiftly on to poking at StackOverflow for "friendly" advice. Eventually I settled on installing another gem, `activesupport`. I made an `inflections.rb` file in my config folder and added the following:
```
ActiveSupport::Inflector.inflections do |inflect|
  inflect.irregular 'dive', 'dives'
end
```
and it looked like my problems were over. And they were for a while, but the next day I was getting the same problems when working within Tux so I found this, admittedly more simple method of simply making an addition in my Models:

Original: `has_many :dives`

Updated: `has_many :dives, :class_name => "Dive"`


### Speaking of Tux, Silver medal goes to....
[Tux](https://github.com/cldwalker/tux). Tux is awesome. It takes your Sinatra application and gets it a new suit so it can join the CLI party. However, when I first went to fire it up, Tux was apparently not yet dressed. In fact, it could not even find the damn suit. It turns out that even when all looks correct, the map is unreadable when you use a require_relative in the config.ru file. After a little frustration,  I simply changed the path to a require and all was well again. *(Note, this is not Tux's fault, it just first became apparent when I went to use it)*

### And Bronze, for an easy fix problem
I started with my project with wireframing the Models part of my MVC pattern. I was a bit too keen though and made up a whole new join table that I thought I needed at the time. Needless to say this caused me great confusion and anguish when building out my models and testing the ActiveRecord associations. The feeling when it dawned on me that this annoying table was in fact superfluous was excellent - I simply deleted all trace of it, adjusted my associations to things that made much more sense and of course it all started working as expected.

## Setting up the structure
I did not use [Corneal](https://github.com/thebrianemory/corneal), mostly becasue I didn't know about it at the time. I'm glad I didn't though because manually making the whole structure from scratch really helped to solidify the exact whats and whys of what I was adding to my clean slate.

## Timeline
<img src="https://i.imgur.com/UXbbrfb.png" alt="timezones" width= "50%" align="right" style="margin-left:10px;">
<p style="text-align: justify;">I made an outline schedule for myself which I almost managed to stick to. I got a bit carried away with adding things here and there, as I expected I would, but on the whole I managed to stick to my self-imposed deadlines, as long as you ignore timezones. (as in, I'm in Australia but decided to switch to the American Somoa timezone for the purposes of this project... Fair.)</p>

## A brief tour
<img src="https://i.imgur.com/xxhj6KK.png" alt="Divesite index" width="33%" align="left">
<div width="33%"> <p> *Left: Divesites index / Right: User show page Right: New Dive form / New Divesite form / Edit User form*</p></div>
<img src="https://i.imgur.com/R52jXGx.png" alt="Dive log"  width="33%"  align="right">



<img src="https://i.imgur.com/oFNHDvf.png" alt="New Dive form" height="348px" align="left">
<img src="https://i.imgur.com/JhYkqtD.png" alt="Update account details" height="348px" align="right">
*Left: New Dive form / Right: Edit User form*

*And the pièce de résistance - my Dive and Divesite show pages with a big beautiful embedded map in the middle
(the Dive show page is similar so below is only the Divesite show page as example)*

<img src="https://i.imgur.com/ukErFDB.png" alt="Divesite show page" width="100%">

Isn't it beautiful? The things I did for that map... Google have my card details now (I expect they did before anyway) and for no actual charge they presented me with an API key which I could use to make cool things like that happen! It is one of my very favourite things about the design and it's also very functional. On the Dive show page, it is set to a zoom level where you can see the site (at least, the results of Google's search against the Divesite name.). On the Divesite page however, it is set to search for the nearest dive centers in the surrounding area to the Divesite! Pretty handy - so if you are perusing the app and see a divesite you'd like to check out, the map is alreayd right there showing the local dive shops. Magical.

## Authenticity
Various validations are in place all over this app. From checking the format of the date (it's DD/MM/YYYY no arguments) to authenticating logins using encrypted passwords (thank you, bcrypt), I ended up with validations in various languages; here are a few examples:

* HTML/Regex: `<input class="triple_column_inputs not_first" name="username" placeholder="Username" pattern="^\S*$" title="No spaces please! how about a hypen or underscore instead?">`
* ActiveRecord:  `validates :email, uniqueness: true`
* Customised ActiveRecord with Regex: `validates_format_of :date, :with => /\d{2}\/\d{2}\/\d{4}/`
* Homemade in Ruby: 
```
 @dive = Dive.find_by_user_divesite_and_date(params)
    if @dive.user != current_user
      flash[:alert] = "You can't make changes to another diver's log!"
      redirect "/#{@dive.user.slug}/#{@dive.divesite.slug}/#{@dive.slug}"
    end
```

I suppose it would have been tidier to keep as much as possible to one type but for these purposes, it was a great excuse to test out implementing validations in various different ways.

## The elephant in the room
This project did not require any fancy front end design. Despite this, I managed to battle with CSS for nearly 2 days before I got to a point where i was happy to present it. My stylesheet is the only file that I've not yet gone to really tidy up, partly because I don't trust it. I feel like things change in there just by looking at it the wrong way.

## Improvements
There are a few features I would love to add in the future for this app.
+ Ability to add and track dive qualifications
+ Ability to 'follow' other divers and see a customised dive feed of only their dives
+ Ability to search for other users
+ Ability to add a dive buddy (another user) to each dive and have the dive connected to both users

## Takeaways
April 6th 2018 I had my CLI assessment, my first portfolio project piece for my Fullstack Web Dev course with Flatiron.
At the time I was exhausted, running on adrenaline and little else. I went in hard and learned a few lessons. Looking back at the equivalent blog post, I found these notes:
> What I will do differently next time:
> 
I will write a test suite. Before writing my code! I I think I will add tests retrospecively to the berklee-valencia gem as an exercise in writing my own tests and also to make my gem more credible.
>
Following up from that point, I will not rush in so hard. I really thought I went in with a solid plan but now experience has taught me that it is worth giving it a bit more time before starting to write code.
>
The whole process will be smoother as hopefully I won’t be re-learning git, bundler and rubygems next time! As did the refactor I also noticed that I was getting a lot quicker at tracing bugs and sometimes seeing errors before they happened. As with any skill I am sure this will keep improving with time and hopefully the face-plant count will decrease with each new project.

Well I'm pretty pleased to say that 
+ a) I **did** write a test suite! ***Before*** I wrote my code!
+ b) I didn't rush in hard. I really thought things out, of course there were bumps along the way but nothing seemed insurmountable and despite a few late nights, I have not totally exhausted myself this time.
+ c) Indeed, the process of just getting started was so much smoother this time. Git was a beautiful tool this time instead of a skittish animal to be wrangled to my will. I have a similar number of commits on each project but I know that the vast majority of the commits in the CLI gem were me battling with git, renaming things and not actually changing much code, not incrementally anyway. This time, every commit was a solid, defined addition or change and that feels fantastic.

In the past month (6 weeks, but I took 2 weeks off go to Bali and get engaged, what a chore!) I have become so much more confident around code and more comfotable with troubleshooting. I no longer do the inside scream when tests fail - I like the tests now, they really do tell you what you need to do. Especially now I'm writing my own - I can write them in a way that I really connect with.

## What next?
Although I'll be sad to have less excuse to listen to Frank Sinatra instrumentals all day, I'm very excited to crack on with Rails! Every day I'm becoming more fluid and proficient at this game and increasingly comfortable with finding solutions to the unknown. Ideation for Project 3 starts now!
# What got me through this project? Tea. Lots of tea.
<img src="https://i.imgur.com/Arocjkw.jpg" alt="tea " width="100%">

