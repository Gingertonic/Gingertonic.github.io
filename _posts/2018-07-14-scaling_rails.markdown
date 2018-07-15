---
layout: post
title:      "Scaling Rails"
date:       2018-07-14 23:35:42 -0400
permalink:  scaling_rails
---

<img src="https://media.giphy.com/media/7zleDqXp959UyA2Wv5/giphy.gif" alt="Scale This!" width="50%" style="margin-left: 25%; border: 1px dashed grey; border-top-left-radius: 20%; border-bottom-right-radius: 20%;">

|  What?  |  Why?   |   How?  |
| -------- | -------- | -------- |
| Scales practise tracker | I love scales! Haha... erm...  | Ruby on Rails! |


### What?
[Scale This](https://github.com/Gingertonic/scale-this) is a a web app where you can manage your scales practise! <br>
Users can view and add to a scales library, log their practise and see who's been practising recently! 

### Why?
I've been practising scales since I was 5 and I've used a million and one different ways to track my progress. Some have been better than others but none have really stuck. I wanted to try and find a web-based solution to this problem held by musicians of all ages and abilities around the world! 

### How?
Handily enough, this seemed to fit well into the brief for our Rails Portfolio Project for the Full Stack Web Dev program at Flatiron School. 
<br>
Using [Ruby on Rails](https://rubyonrails.org/), [OmniAuth](https://github.com/omniauth/omniauth), a sprinkling of [web audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API) and [some other ingredients](https://www.google.com/search?tbm=isch&source=hp&biw=1280&bih=703&ei=XMdKW9ODHoni8wXG6o-4CA&q=tea&oq=tea&gs_l=img.3...793.942.0.1111.4.4.0.0.0.0.0.0..0.0....0...1ac.1.64.img..4.0.0.0...0.Vq-R9Hbb5Ps), I've just finished the first completed draft.



<br>
## Structure
We were under strict orders not to use [scaffolding](http://guides.rubyonrails.org/getting_started.html#getting-up-and-running-quickly-with-scaffolding) for this project and honestly I can't see why you would ever wish to use it. Scaffolding a Rails app gives you a bunch of extra stuff you probably won't need or understand. And if you understand it, there's no reason youcan't just create it yourself later when you definately know you need it. Scaffolding, in my humble opinion, is messy.

Even just the regular Rails app creation gives you thing you don't necessarily need. It's quite cathartic to go through getting rid of them once you've realised they're not magical files of unknown - they're just empty files taking up real estate in your side bar.

I have four models: Musician (user), Scale, Practise and Note.

|                                 Musician                             |                                          Scale                                   |                   Practise             |   Note   |
| ------------------------------------------- | ------------------------------------------------ | -------------------------- | -------- |
|                     `has_ma ny: practises`             |                      `has_many: practises`                     | `belongs_to: musician` | no AR  |
| `has_many: scales, through: practises` | `has_many: musicians, through: practises` |     `belongs_to: scale`    | associations |
|    controllers, views, even stylesheets    |                everything, even JavaScript!              |            controller only        | no extras |

As you can see, if I had scaffolded these, I'd have a LOT of extra stuff I didn't want. 


<br>
## Challenges
I faced quite a few challenges of varying complexity during this project but on Day 1 I was faced with three big ones that were core to the success of the idea:

#### How the hell do I teach a computer scales?
This was extremely important and after a few cups of tea I came up with some thoughts:
* each note has a midi value which increments by 1 for every semitone. Quartertones are more and great but let's leave that for the future.
* each scale will have a pattern expressed as a string of numbers eg "2212221" for "TTSTTTS" (a standard major scale in tones and semitones notation)
* therefore a user can choose a scale (eg Major ("2212221") in Semitone counts) then choose a root note (eg middle C (60 in midi)). Using the pattern, the app can create a scale starting on note 60 and use the pattern to add the other notes:
  `60 (+2) 62 (+2) 64 (+1) 65 (+2) 67 (+2) 69 (+2) 71 (+1) 72 `
  which is C Major scale in midi note values!
	
Great. I was ready. But this was going to need a bevy of custom methods (dare I say it... algorithms?) to get this to actually be useful. Here are a few of my favourites that I came up with and are now implemented in the app:
```
   def scale_generator(root, octaves) #returns the frequencies of a scale pattern calculated from the given root note
    frequencies(root, octaves)
  end

  def see_notes(root, octaves) #returns the notes as a scale pattern calculated from the root note
    notes = []
    midi_generator(root, octaves).each do |midi_value|
      notes << Note.find_by(midi_value: midi_value).solfege[0...-1]
    end
    notes
  end

  def frequencies(root, octaves) #helper method for scale_generator
    frequencies = []
    midi_generator(root, octaves).each do |midi_value|
      frequencies << Note.find_by(midi_value: midi_value).frequency
    end
    frequencies
  end

  def midi_generator(root, octaves) #returns the midi values of a scale calculated from the root note
    degrees = []
    pattern.split("").each do |st_count|
      degrees << st_count.to_i
    end
    midi_array = [root]
    degrees.each do |st_count|
      midi_array << midi_array.last + st_count
    end
    if octaves == 2
      octave_two = []
      midi_array.each do |note|
        octave_two << note + 12
      end
      midi_array.push(octave_two).flatten!.uniq!
    end
    midi_array
  end
```
	
The  addition of the second octave is not implemented in the front end at the moment but the code is there ready for if/when it makes sense to add this.

My personal favourite method in the app is this one:
```
  def i_just_practised(params) 
    new_practise = self.practises.find_or_create_by(params)
    new_practise.increase_experience
    new_practise.save
  end
```
or maybe this one
```
  def not_your_scale(current_user)
    private && created_by != current_user.id
  end
```

I like naming methods in ways that make me smile.

<br>
#### How can I represent a scale on a computer screen in a way that is accessible to all?
This was another big one. Of course there are a few 'standard' ways to represent scales visually but the one I know best (the 5 line stave) is not readable by all. It is another language, a graphical one, which needs to be learnt.

How do you see music notation?

<img src="https://media.giphy.com/media/l3q2HJ8XvY1aCbNKg/giphy.gif" alt="music notation" align="middle" style="width: 25%; border-radius: 50%; margin-left: 20%"><img src="https://media.giphy.com/media/8lPSqcjcNjymIOS4Pm/giphy.gif" alt="music notation" align="right" style="width: 25%; border-radius: 50%; margin-right: 20%">

<br>
<br>
<br>

So I decided to draw from solfege, it's not something I use a lot in my musical thinking but it's not so unfamiliar to many people - mostly thanks to the *[Sound of Music](https://www.youtube.com/watch?v=pLm07s8fnzM)*!

What's [solfege](https://en.wikipedia.org/wiki/Solf%C3%A8ge)? 
<img src="https://media.giphy.com/media/85SCvLPXnhb8s/giphy.gif" alt="Sound of Music" height= "150" align= "right" style="margin-right:100px; border-radius: 50%;">
* Do
* Re 
* Mi 
* Fa 
* So 
* La 
* Ti....

Those are the 'major diatonic' solfege notes. There's a few more to cover all your bases (there are 12 notes altogether).

So each Note in my database has:
* `midi_value` (used for audio plaback, and has very handy for my algorithm to convert a numerical pattern into a scale) more info on [midi here](https://en.wikipedia.org/wiki/MIDI).
* `name` (the name used commonly in English eg C or C# (c sharp)
* `solfege` (eg. do, re)
* `frequency` (calculated at [equal temperement](https://en.wikipedia.org/wiki/Equal_temperament) from [A=440](https://en.wikipedia.org/wiki/A440_(pitch_standard)) (not used in my current version of the app but always handy to have on hand.)

Combined with some fun and games with [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API) (which I won't go into here as it was not a requirement of the project), my scales are represented like so:

<img src="https://media.giphy.com/media/46zGtlFCNsOVNLY6PA/giphy.gif" alt="scale playback" width="100%">

Clearly this is primarily a question of User Experience and not the focus of this project but it was very interesting problem to have to solve and one which I was only able to answer with personal opinion, not user feedback (yet). There are numerous improvements that could be made but this is more a question of music education and UX!

<br>

#### How can I track a user's experience with a scale?
Initially I was thinking to have a new instance of a Practise created every time a Musician (user) practised a Scale, regardless of whether they had practised that scale before or not. It became clear that this would be somewhat inefficient and so I changed my approach to have a new Practise created only the first time a user practises that specific scale. <br> <img src="https://i.imgur.com/sTWQtmq.png" alt="last practised" height= "150" align= "right" style="margin: 10px;"> 
<br>
For subsequent practises of that scale, the Practise instance for that user and scale will have its experience attribute increased by 1. With this, we can easily query how many times a user has practised that scale.


I wanted to also track *when* a user last practised. It's all very well having practised 100 times but if that was 6 months ago it's not quite so useful today! I utilised the updated_at timestamp on the Practise model when writing methods such as this:

```
  def status #returns when the practise last happened
    if easy_read(updated_at) == today
      'today'
    elsif easy_read(updated_at) == yesterday
      'yesterday'
    elsif last_practised.to_i >= this_week
      'this week'
    elsif last_practised.to_i >= last_month
      'this month'
    elsif last_practised.to_i < last_month
      'ages ago!'
    end
  end
```

<br>

#### How can I compare users' progress?
To satisify the Type As, I wanted to add a rankings list. Savage but also kind of fun.
It sounded easy enough but it took me a little time and revision to get my AR queries correct. I wanted a user to be able to order rankings by name (alphabetically), total practises logged and by who most recently practise.

<img src="https://media.giphy.com/media/3XAUZCNIz0yFmv6D2f/giphy.gif" alt="rankings demo" width="70%" style="margin-left: 15%; margin-right: 15%;">

The queries I used for this were:
 * Name: `where.not(name: 'Admin').order("LOWER(name)")`
 * Total Practises: `joins(:practises).group(:musician_id).order("sum(experience) desc")`
 * Last Practised:  `joins(:practises).group(:musician_id).order("practises.updated_at desc")`


<br>
## A few road blocks I found on the way

- `:type` can't be an AR database column name - until I renamed to `:scale_type` there were frowns

- Web Audio API is not a walk in the park if you've not done much JS. I am very grateful for this [Web Audio Basics repo ](https://github.com/kylestetz/Web-Audio-Basics) with demos from which I learned a lot.

- Soundcloud is not currently accepting new apps! I originally hoped to enable third party authentication via Facebook and Soundcloud. Currently I have only Facebook and local signup/login available since Soundcloud is not accepting new apps at the moment! It would be great to add in the future.

- Timezone issues. If I practise a scale early morning here in Cairns, Australia, it thinks I practised it yesterday! Fortunately most of my friends and colleagues are in Europe and America so living in the future isn't something that will affect them! A bug to fix in the near future.


<br>
## Validation and Authentication
#### OAuth
I had a good time working with OmniAuth and the Facebook API. It can be quite finicky but really once you've done it once it's fairly straight forward. I intended to add Google OAuth but the process was slightly different and I will add this at a later date. I was more upset that Soundcloud was not possible (see above!) as it's a very relevant platform to have related to my app.

#### Local signup/login
I didn't want 3rd party authentication to be the only option. Up until recently I never used 3rd party authentication (I use it all the time now, although I'm picky about what permissions I give) and I know that many people will still not use it. I also wanted the app to be accessible to all ages and there's a lot of people, especially younger and older generations who do not have social media accounts.

#### Data validation
In my last project I used a variety of different forms of validation. Partly to practice them and partly because I didn't really know what I was doing. This time I tried to keep my validations much tidier, more effective and less vulnerable. I relied heavily on AR validations and the handy full error messages method to display my custom error messages without adding lots of extra lines of code as I did in the last project.

I did add some custom validations eg. into the process of creating new Practises. I believe this could be streamlined further but I chose to go this route for now.

#### Permissions
As I gave the user the option to make any scale they create private or public, I needed to be able to navigate this when displaying the scale library and also not let a user sneakily access a private scale by manipulating the url.
Whilst an index page might often just be populated by a `@scales = Scale.all` variable, I went with `@scales = Scale.custom_index(current_user)` which calls this method which returns a list of scales visible to the user (based on permissions and private/public scale status)
```
def self.custom_index(user)  
    Scale.all.select{|s| s.private == false || s.created_by == user.id}.sort_by{|s| s.name}
  end
```

If a user does try and access a private scale directly via the url, they are redirected back to the index where they see a flash error saying 'Hey, that's private'!

Some scales can be seen but not edited (a user can only edit a scale that they created). I check for this using this custom method (which calls another custom method, `valid_scale` which checks that they are allowed to view the scale first)
```
  def editable_scale?(scale)
    if valid_scale?(scale) && scale.created_by != current_user.id
      go_to(scale, root = "do", alert = "You can't edit this scale, sorry!")
    end
  end
```

It also uses `go_to(scale, root, alert)` which I made since I realised that I was typing this lengthy redirect_to more often than I ilked:
```
def go_to(scale, root = "do", alert = nil)
    redirect_to show_scale_path({scale_slug: scale.slugify, root_note: root}), alert: alert
 end
```

<br>
## Staying DRY
I regularly went through all my code systematically (Models, Controllers, Views) to check for [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)ness. The Scale related files are all quite busy but I believe they are as DRY as I can make them to my best current understanding. The Scale show page was particularly ugly at first but I took a lot of it out into the Scales helper (as I did for many of the other views too). I became fairly familiar with `content_tag` and its various quirks. Nesting content tags within content tags is a bit tricky and I am sure there is more to learn here. I am happy with the result at the moment.

I also made use of partials for the forms and also error rendering. This was the first time I had utilised local variables in partials  eg: `<%= render :partial => 'layouts/errors', locals: {obj: @scale} %>` which I found extremely useful. I also used this in rendering my form partials in order to change the automatic submit tag text from eg: "Create Scale" to just "Create": 
`<%= render :partial => 'form', locals: {submit_text: "Create"} %>`


<br>
## Progress from previous large project

#### Timeline
All in all, this has been an 8-day project (today is day 9, paperwork day!). Compared to my last portfolio piece, I spent much more time actually coding this time. Whilst making my Sinatra web app, GROTTO, I seemed to hit a roadblock every hour or so. I still hit knowledge gaps and gaping questions whilst making Scale This, but I am now much more fluent in problem solving. My ability to find the relevant documentation and locate the info I need from it, is markedly improved.

#### CSS
I can't even recognise myself in CSS land compared to the last project. Last time I was legitimatelly scared of CSS, I didn't trust it let alone understand it. Between then and now I've been practising CSS Diner and Flexbox Froggy which have been invaluable in improving my fluency and understanding of CSS.
 
#### Staying calm and having fun
My improvements gave me the opportunity to be more creative and address questions of user experience, best practises and experiment, without feeling I was jut clawing my way to producing anything I could.

 
<br>
## Future Improvements / What next
For this specific app, there are certainly many improvements to make and fortunately I will be able to address some of these soon when we revisit this project to officially add JavaScript. 
 
It still amazes me how much I am learning, when I compare myself just to last week I have improved my understanding of Rails principles drastically. Comparing myself to last project, I am more fluent and thinking more efficiently. Comparing myself to the start of this year, well, in January I was patting myself on the back for getting 2+2 to equal "Mickey Mouse". 

The progress is so exciting and the more I learn and do, the more creative freedom I have to make whatever my brain decides it wants to!

<img src="https://media.giphy.com/media/GQHiM54keVfQk/giphy.gif" width="100%">
 
 
 

 
 


