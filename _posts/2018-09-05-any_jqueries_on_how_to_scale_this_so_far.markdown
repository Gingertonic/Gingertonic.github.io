---
layout: post
title:      "Any jQueries on how to Scale This so far?"
date:       2018-09-05 07:51:48 -0400
permalink:  any_jqueries_on_how_to_scale_this_so_far
---


Here I am, a whole week later than I had hoped, with a fully functioning jQuery-powered, AJAX-pixie-dust-fuelled version of my app *Scale This*. I have also developed a caffeine dependency.

<img src="https://media.giphy.com/media/wapxtMxV2XMwo/giphy.gif" alt="Any tea?" width="50%" style="margin-left: 25%; border-top-left-radius: 20%; border-bottom-right-radius: 20%;">

And why, pray tell us Beth, are you a week later than anticipated? (incidentally, that is the same question my gym trainer asked me on Monday...) Well partly because I was waking up through the night barely breathing and leaving snot-trails around the house for a week (TMI? You're welcome.) Partly because I'm living in a very popular tourist town and visitors are relatively plentiful.

But mostly... mostly because THIS STUFF IS HARD! and SOMETIMES WEIRD! and the previous couple of weeks I've been feeling somewhat intellectually plateaued. 

I've come to realise that a good tidy up and refactor of your work is a great way to revise what you did, gives you a chance to look at things and say 'what sort of amateur did this!' (and realise it was you, probably yesterday, so give yourself a pat on the back for coming so far overnight but also maybe hold off a bit on the high and mighty, thanks)

So after a good 48 hours tidying and refactoring, I feel like I do actually have a decent grasp on the new concepts introduced for this project, but it was an epic journey.

Seeing as this project was a re-work of my previously discussed *Scale This* app made using Ruby on Rails for front and back end, I will invite you to read [my blog](http://thegingertonicstudios.com/scaling_rails) on that for more about the idea behind the app.

This new, improved, [Nando's extra-hot sauce](https://www.nandos.com.au/eat/products/extra-hot-peri-peri-sauce) version of *Scale This* has got rid of the bulky Rails front end and replaced it almost entirely with Javascript. Woah! The backend is similar to before but now it serves as a Rails API which my shiny new JS front-end just makes calls to in order to get the data it needs. 

### Backend changes
The Database hasn't changed one bit (thank God, because the last time I had to convert my SQLite database to PostgreSQL I nearly threw my laptop out of the window)

The Models have been on a serious anti-bloat diet. I still need them but I was able to relieve them of some of their respective methods and move that functionality to the front-end JS Object Prototypes (more on that later).

The Controllers are much lighter now. Their only functionality now is to feed data to the front end. Which, of course, not different than before but previously the frontend Views and the Controllers spoke a lot more verbosely to each other. Now, the front-end calls the the controllers, says 'I want that one', the controller gets that one from the database, gives it to the front-end and then they don't speak again until they want something else. The front-end is somewhat more independent now.

### Frontend changes
Those Rails views are all but gone. Of 12 views (plus a partial) I kept 4 of them - a landing page, the sign-up page, the login page and the scales index page which has now turned into an all-singing, all-dancing Almost-Everything page.
They have been replaced with what could be just 1 long JS file but because I like nice, neat, organised code, is actually 11 JS files plus 7 Handlebars templates. When I put it like that, it sounds like a backwards leap but when you think that all those 18 files could also work as 1 long, ugly file, and actually run the app, that's pretty cool.

<img src="https://media.giphy.com/media/JFawGLFMCJNDi/giphy.gif" alt="I love changes" width="50%" style="margin-left: 25%; border-top-left-radius: 20%; border-bottom-right-radius: 20%;">

## Dictionary of Useful Things
### AJAX
[AJAX](https://www.w3schools.com/xml/ajax_intro.asp) stands for Asynchronous Javascript and XML. 
- The **Asynchronous** refers to the fact that we can make an AJAX request and then leave it to it's business whilst we get on with ther things, which is pretty awesome and way more fun than waiting around for a full HTML page load.

- The **Javascript** is there because we use [Javascript](https://www.javascript.com/) to make the request. In jQuery flavour, an AJAX call sending info regarding a potential New Scale could look something like this:
```
$.ajax({
     url: '/scales',
	 method: 'post',
	 data: params
	})
```

or if you're feeling a bit lazy and don't need to add any extra options:
`$.post('/scales', params)`

(for PATCH and DELETE requests, the shorthand of the second example is not available.)

It's possible in vanilla JS too of course, although things get a little bit ugly. By all means go forth and [investigate](http://lmgtfy.com/?q=ajax+with+vanilla+javascript), but don't say I didn't warn you.

- The **and** is a necessary [conjunction](https://www.englishgrammar.org/conjunctions-4/).

- The **XML** is there because [AJAJ](https://www.howtopronounce.com/ajaj/) is weird to say out loud. See, you just tried it and it was weird, right? XML used to be the standard format of an AJAX response and it still is sometimes, especially in some older APIs. More recently however, responses most commonly come in the JSON (Javascript Object Notation) format. 

### jQuery
[jQuery](https://jquery.com/) is a little Javascript library which is so remarkably awesome that it is practically ubiquitous on today's web. It can achieve this:

**Vanilla Javascript**
```
function fadeIn(el) {
  el.style.opacity = 0;

  var last = +new Date();
  var tick = function() {
    el.style.opacity = +el.style.opacity + (new Date() - last) / 400;
    last = +new Date();

    if (+el.style.opacity < 1) {
      (window.requestAnimationFrame && requestAnimationFrame(tick)) || setTimeout(tick, 16);
    }
  };

  tick();
}

fadeIn(el);
```

with just this:
**jQuery**
```
$(el).fadeIn();
```
*example taken from [this great article](https://www.codementor.io/brainyfarm/jquery-vs-vanilla-javascript-deciding-on-what-to-use-6b79xdmrv) looking at when to use jQuery and when to use vanilla JS*

Pretty nice, right? It's not always the best tool for the job as, whilst it's very popular, it's not supported *everywhere* and being an 'add-on' to JS, it can slow performance a bit. Not so much that this bothers me in the slightest on this app. Some people seem to get very snobby about it and get their knickers in a twist about jQuery. I think that's  kinda funny.

<img src="https://i.imgur.com/40l3evg.png)" alt="I heard you like Javascripts" width="50%" style="margin-left: 15%;">

<img src="https://i.imgur.com/R7jlmmO.jpg" alt="tell me more" width="50%" style="margin-right: 15%;">


### Vanilla JS
This is the term used for plain old Javascript with nothing extra, no fancy libraries, nada. It's incredibly web-friendly and it works fastest when alone. jQuery is not always the best tool and it's wise to stick with vanilla JS whenever it makes sense to do so.

### ES6
ES6 is a name bandied around when referring to [ECMAScript 2015](https://www.w3schools.com/js/js_es6.asp). Apparently some people also call it Javascript 6 which does kind of make sense and perhaps with that no more explanation is required.
With the ES6 update came some [Cool Things](http://es6-features.org/) like Consts and Lets, Arrow Functions, Template Literals, Classes and quite a few more.

### API
API stands for [Application Programming Interface](https://en.wikipedia.org/wiki/Application_programming_interface). Sometimes, when we have a database-driven application, we may want to get that data to various different places; perhaps we have a web app as well as a mobile app, perhaps we want to make some of the data available to other websites. There are various uses. 
Whatever your reason for wanting to get the same data to different places, it would be mad to make a brand new back-end to support each different front-end. Not only would it be time-consuming in the first place, it would also be a nightmare to update all of them. 
So we can use an API instead. With your API in place, you can make a request to it and receive back only data. That means  no extra baggage like HTML or CSS. Just plain old data with which you can do whatever you desire once received. You don't need to dig through all the extra stuff just to find the name of the current number 1 song in Chile. Instead you can just make a request to `https://api.number1songs.com/chile` and receive back something like `{ date: 20180805, title: "Vaina Loca", artist: "Manuel Turizo & Ozuna" }`. Too easy.

### Handlebars
[Handlebars](http://handlebarsjs.com/ is ridiculously useful and at times ridiculously frustrating library for making templates. At first I thought it was just me but I've since found that it has something of a a reputation among the Flatiron community for being the source of many a lost hour wondering WHY? We forgive it for all this because it gives you handlebar mustaches all over your code.


<img src="https://media.giphy.com/media/11UzbTpybT6Ypy/giphy.gif" alt="Mustache approved" width="50%" style="margin-left: 25%; border-top-left-radius: 20%; border-bottom-right-radius: 20%;">



## The Requirements
### 1. Must render at least one index page (index resource - 'list of things') via jQuery and an Active Model Serialization JSON Backend
When a User visits the Scale Library (oh, anyone can see that now, I thought was a nice freebie for anyone who likes scales but doesn't like creating accounts, [even if it is dead easy with Facebook OAuth...]), they are presented with a nicely laid out index of Scales, sorted into their Type categories. Cool, no big deal, nothing special. Until one time, when you're viewing a specific scale then you return to the Library (the scales index) and you realise that THE PAGE DID NOT REFRESH! No sir, it did not. It changed, fairly dramatically, replacing the nice scale dots with the same categorised lists of scales that you saw before, but you are on The Same Page. Cool! But how?! Well, when you clicked on 'Scales Library', it did not actually make an HTML request. Instead, we `e.preventDefault`-ed that, hijacking it to not let you go anywhere at all. In fact, instead of making you go to a different page with the information you want, we (we being the dream team of jQuery and my Rails API) bring the information directly to you. Don't you or your browser dare go anywhere, it would veritably offend us.

Whilst you sat back with your tea, jQuery made a quick phone call (er, I mean, a get request (via AJAX)) to the API where he was redirected to the scales#index office who swiftly provided him with a custom list of scales for the current user, and was even so kind as to have the information translated for him by an in-house Active Model Serializer which will translate data into JSON (Javascript Object Notation) so it's ready to go when it hits the front-end.

jQuery, armed with the new information, goes through it, makes a new Scale object for each scale, figures out where it should be placed on the page and puts a nice link to the scale where it belongs.

### 2. Must render at least one show page (show resource - 'one specific thing') via jQuery and an Active Model Serialization JSON Backend. 
Similarly to the scales index, when a user clicks on one of those links, they still don't have to go anywhere. Instead, jQuery makes another call to the API, this time asking for all the data on a specific scale. The API retrieves the scale from the database, translates it to JSON and returns it to jQuery. Using this data, jQuery renders the scale in the same two containers as the Scales Library had been displayed.

This same call and response cycle is made when a user clicks on a link to a scale from their own Practise Log.

### 3. The rails API must reveal at least one has-many relationship in the JSON that is then rendered to the page.
When a user views a specific scale, jQuery doesn't just request data about the scale, but also about the current user. It asks for more than just the basic data about the user however. The API must also provide information on the user's practises. In the database, Musicians (users) get a `has_many` relationship which links them to the practises they have done. The front-end receives this information and uses it to show the user how much practise they have done of that specific scale! That way, if you see 'Practised just once...', you may get the inspiration to practise it again... and again... and again...

### 4. Must use your Rails API and a form to create a resource and render the response without a page refresh.
The user is able to create a new scale or pattern with whatever notes they like, as long as that pattern has not already been saved under another name. The nice thing about making AJAX requests is, once you've got the data back from the API, you can do whatever you like with it, without refreshing the page. In this case, when you hit submit on the New Scale form, the form is sent off to the API which, if everything looks good, creates a brand new Scale in the database and then sends this brand new scale back to us on the front-end. When we get it back, jQuery just adds a link to the library withour refreshing the page. It also clears the New Scale form so you can keep adding more scales until you're over it. Then you can go and visit any of those scales by clicking on the shiny new link that was created each time you made a new scale. And all this without refreshing the actual page a single time! If the form data can't be used to make a valid scale, the API sends back the list of reasons why not (errors) and then jQuery renders each error in a big red box to make sure you know you screwed up. Without refreshing the page, of course.

Likewise, if you are viewing a scale for which you edit permissions, you have access to an Edit Scale form. When submitted, the scale updates automagically (an by automagically, I mean with jQuery) right in front of your eyes.

### 5. Must translate the JSON responses into Javascript Model Objects. The Model Objects must have at least one method on the prototype. 
The sad thing about saying goodbye to some of the functionality my Rails Models, is that, at first glance, you would be forgiven for thinking it will be a lot harder to manipulate data in Javascript without these handy Models.

Well. In ES6, JS added the glorious feature of Classes. They're really just functions which do cool things. It is not dissimilar to the idea of making Models in Rails. They are very handy ways to create an instance of a Thing which automagically provides it with some custom methods.

For example, in Scale This, when my front-end receives data about a scale from the API, it uses that data to make a new Scale Object. So say I have received the attributes of a scale in JSON
eg: 
```
 attributes = {id: 23, name: "cool scale", scale_type: "super awesome", origin: "unknown", melody_rules: "only play penultimate note on Tuesdays", private: false, pattern: "211212", created_by: 4}
```

I can pass this info via `const coolScale = new Scale(attributes)` to the following Class constructor function:

```
function Scale(attr){
  this.id = attr.id
  this.name = attr.name;
  this.scaleType = attr.scale_type;
  this.origin = attr.origin;
  this.melodyRules = attr.melody_rules;
  this.private = attr.private;
  this.pattern = attr.pattern;
  this.aka = attr.aka;
  this.createdBy = attr.created_by;
}
```

where it will create a new Scale object and assign it to the variable `cool_scale`.


<img src="https://media.giphy.com/media/l0HlDtKDqfGGQtwic/giphy.gif" alt="There's more..." width="50%" style="border-top-right-radius: 20%; border-bottom-left-radius: 20%;"><img src="https://media.giphy.com/media/l0Exdm9UbTHAFcJi0/giphy.gif" alt="There's more?" width="50%" style="border-top-left-radius: 20%; border-bottom-right-radius: 20%;">



Without you knowing, I actually already created a bunch of methods that Scales can do like these:

```
Scale.prototype.patternFrom = function(root){
  patternFrom = [root];
  for (let i=0; i < this.pattern.length; i++) {
       diff = parseInt(this.pattern.charAt(i));
       patternFrom.push(patternFrom[patternFrom.length - 1] + diff);
     }
  return patternFrom;
}

Scale.prototype.scaleTypeSlug = function(){
  return this.scaleType.replace(/\W/g, "_");
}
```

Now, because coolScale is an instance of a Scale object (as defined by yours truly), I can call `coolscale.scaleTypeSlug()` and I will get back `"super_awesome"` which will make a good id attribute for a div on my scales index page to house all the scales which are also of the type Super Awesome!

I also have a Musician class in this app so I can get the data about a user from the API and use it to make `const gingertonic = new Musician(data)`

So newUser doesn't have access to the Scale functions above - `newUser.patternFrom(60)` would be thrown back in our faces. But don't despair, I gave Musicians a nice function that tells us how much practise they've been doing!

`newUser.totalPractises()` will call:

```
Musician.prototype.totalPractises = function(){
  let totalExperience = 0
  this.practises.forEach(practise => totalExperience += practise.experience)
  return totalExperience
}
```

on `gingertonic` and hopefully give us back a very high number because I practise a lot... heh....



## Round-up
Initially it was a bit of a rude shock to step out of Ruby-land and back into Javascript. It had been a good 7 months since I last really used Javascript for much and it felt a bit like trying to write an essay in a subject you know very well, but in a foreign language that you used to speak a bit of but not much you've basically forgotten most of it anyway. 

I must say, I do think jQuery is pretty damn cool and I also like some of the ES6 features which I incorporated into this application.

Every time I complete a project, I look back on the previous one and think how incredibly clunky it looks in comparison to my new one. I can only assume that moving into React/Redux, I will experience the same cycle of WTF WHY? => Eh, I get it but... why? => WHY DID I NOW KNOW THIS BEFORE? I SHALL NEVER LOOK BACK!

And thus I embark on what I hope will be my final month before graduation from Flatiron, but the first month of the rest of a lifetime of coding and learning!




<img src="https://media.giphy.com/media/R2m2NzVxQ3pbG/giphy.gif" alt="I am this close" width="50%" style="margin-left: 25%; border-top-left-radius: 20%; border-bottom-right-radius: 20%;">









