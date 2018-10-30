---
layout: post
title:      "Divine Inspauration"
date:       2018-10-30 17:41:24 +0000
permalink:  divine_inspauration
---

<img src="https://media.giphy.com/media/pHXGCfTPsHKIyGrjkq/giphy.gif" alt="Inspaural instructional gif" width="50%" style="margin-left: 25%; border: 1px dashed grey; border-radius: 4px">

|  What?  |  Why?   |   How?  |
| -------- | -------- | -------- |
| Inspirational audio studio | Who doesn't love an inspirational quote? | Rails API & React-Redux front-end |


### What?
[Inspaural](http://inspaural.herokuapp.com) is a a web app where you can select and mix inspirational tracks to create your own inspirational soundscape, or 'Inspaural'! Users can create, edit, view and delete inspaurals! Each inspaural has 1 'ambience' (backing track) and up to 4 quotes. 

### Why?
I really wanted to make my final Flatiron School portfolio project something that I would be interested in developing out 'in the wild'. My 'pre-code' life as a performing musician and AV technician is still with me and one my goals when I set out learning to code was to be able to create new forms of presenting audio visual material. 9 months after declaring that goal to my Educational Coach, I have deployed an app which I'm really quite proud of. Of course it is not perfect and there is much that I will improve and update but when I sit back and think about the bigger picture of my short and intense journey to this point, frankly I'm rather proud of myself.

### How?
The freedom offered for this final project meant that I had space to think of something a little different although it was actually the React framework which made this relatively easy to implement.
<br>
The backend is on a custom [Ruby on Rails](https://rubyonrails.org/) API whilst the front-end client is made with the [React](https://reactjs.org/) framework and I drew on the Redux store pattern to make things smoother where required.

As this project features audio playback, one of my first questions was how best to implement this. In my first project with a Javascript frontend, I used the WebAudio API which is a power house of awesomeness. I wanted to try something different this time and found several options for npm packages which looked interesting. I went for [react-sound](https://www.npmjs.com/package/react-sound) since it was an easy setup without too many extra options to get caught up in and distracted from the core project requirements. Another package [react-redux-webaudio](https://www.npmjs.com/package/react-redux-webaudio) is on my list to check out in the imminent future.

<br>
## Structure
The project requirements stated that we should use the `create-react-app` generator to get going. It is a [handy little tool](https://github.com/facebook/create-react-app) that gets you up and running swiftly.

For the API back-end, I setup a basic Rails app but with the api-only option which leaves out a few things to streamline everything a bit.

In development I had the client folder containing my React app, stored within my Rails API root folder. Combined with a stated proxy address, this made running it in development super easy. However, when I prepared to deploy to Heroku I separated the api and client giving them individual git inits and therefore they are running as two separate apps which just happen to talk to each other when in use. These separation did mean I had to handle the cross-origin issues but this was easily solved with the `rack-cors` gem.

I have three fully implemented models: Inspaural, Quote and Ambience. I also have a User model ready to implement in v2 of the app in which I will add ability for users to create personal accounts.

|                                 Inspaural                             |        Quote        |                   Ambience             |   User   |
| ------------------------------------------- | ------------------------------------------------ | -------------------------- | -------- |
|   `has_and_belongs_to_many: quotes`, |    `has_and_belongs_to_many: inspaurals`  | `has_many :inspaurals` |`has_many :inspaurals` |
| `belongs_to: ambience`  |  |        |                |
|    [ `belongs_to: user` ]     |                    |                   | |


My API routes lead us to methods in a Inspaurals controller, a Quotes controller and an Ambiences controller. These are safely stored and namespaced in /api/v1/ which means that if I choose to release a v2 of the API, v1 can still be accessed if needs be without writing over it.

<br>
## Challenges and requirements
Contrary to how I aniticipated I would feel now, this project has in fact been the smoothest of all. I am sure I read through the requirements of this back in Febraury on day 1 and felt a certain degree of disbelief that I'd ever be able to understand what they were even talking about let alone produce something. The reality is, I read them and could fairly easily and quickly understand how to implement them.

#### "The code should be written in ES6 as much as possible"

Thanks to a period of utter confusion during my previous project regarding what exactly ES6 was and was not, I had turned to the well-known Udemy course , [ES6 Javascript: The Complete Developer's Guide](https://www.udemy.com/javascript-es6-tutorial/). I've not finished it yet but just a few lessons in and it started to click. I enjoyed using it across much of this project although in some places I decided against it for clarity.

<br>

#### "Your app should have one HTML page to render your react-redux application"

No problem. When using create-react-app as a generator, you get a boilerplate index.html from which your whole app is viewed. The user may think that they are changing pages but in fact they are they are seeing changes in only a a virtual DOM (Document Object Model) and not actually going anywhere. Even if the route changes, we are in fact still on the same original HTML page.

<br>

#### "There should be 2 container components"

At this point I should clarify that the final 'requirement' is *"Go wild! These are only the basic requirements — you're free to add on as much stuff as you'd like."* And that I did since as of now I have 6 container components. These are components which could be considered 'smart' in a way since they can change things and usually have state.

<br>

#### "There should be 5 stateless components"

Actually I currently have 7 although there is potentially scope to make it 8. Stateless components are usually presentational components which simply return some jsx to be turned into html. It can't make any alterations to data.

<br>

#### "There should be 3 routes"

With the assistance of [react-router](https://www.npmjs.com/package/react-router), my **5** routes are:<br>
`/`<br>
`/mixer`, <br>
`/ambiences`<br>
`/my-inspaurals`<br>
`/save`<br>

Note that I do not have a `/quotes` route as might have been expected. The quotes are always accessible, the route changes only effect the content of the inner display of my app.

**Note that this is referring to the React client part of the app. The API has a few more routes!**

<br>

#### "Use Redux middleware to respond to and modify state change"

[Redux](https://redux.js.org/) was extremely useful in this app. It allows us to keep a central 'store' of data which can then be accessed from various points around your app.  One of my favourite things about Redux is that on the Redux homepage, they declare the various features including a "time traveling debugger." I don't know about you but I need no further convincing.

<img src="https://media.giphy.com/media/l1IYhPKrQqn8nnFkc/giphy.gif" width="100%" alt-"time travel">

<br>

#### "Make use of async actions to send data to and receive data from a server"

Since I was serving up the data required to run this app from a separate location (my API server), I needed to implement some successfully asynchronous functionality which would allow us to make API calls smoothly without our timelines getting mixed up. [redux-thunk](https://www.npmjs.com/package/redux-thunk) is invaluable in these situations as it allows us to create asynchronous actions by way of allowing us to use redux's `dispatch` in our action. This is great as it makes it possible to dispatch eg. a "loading" action initially, then make the API call with `.fetch()`, await the response and when the promise made is fulfilled we can dispatch another action with the newly received data as an argument.

<br>

#### Styling

I enjoyed the styling of this app and had it in mind from the very start. This is the second app that I've started out with wireframes and they are now an essential part of my workflow. Nothing fancy is required, just an outline of a vision that I'm aiming for. I find it very motivating and if I get stuck, I will go back to the wireframe and remember what my initial plan was. I have been using the free and simple [wireframe.cc](https://wireframe.cc) and it has served me perfectly well so far.

<img src="https://i.imgur.com/IdshzJz.jpg" width="100%" alt="inspaural studio wireframe">

<br>

## Improvements
- In the near future I intend to improve on this app by adding User login features where Users can save their inspaurals privately or publicly. I wil implement this with options for a local sign up, Facebook and Google.

I am keen to take this concept and make it my first mobile app piece. The API I have built for this should be able to accept and repsond to calls from any platform so I just need to make a mobile-app version of the front end. What a great excuse to try out [React Native](https://facebook.github.io/react-native/)!


 
<br>
## What next
This is it! I've nearly graduated from the [Flatiron School](flatironschool.com) Full Stack Web Development Program!

I have some exciting things coming up that will help me along they way and my aim is to be creating awesome web applications for cool people and companies (myself included!) and also helping other programmers along their journey!

<img src="https://media.giphy.com/media/FZKg2f6KjzkhW/giphy.gif" width="100%" style="border-radius: 10px;">

<br>

There's been an awful lot of Life happening these last two months and oftentimes I've turned to code to keep me sane (perhaps my friends would argue the opposite). So from Belgrade, Serbia, this is one very tired, full-of-cold-and-sore-throat #StudentForLife saying Good Night and I hope to see you on the other side of GRADUATION!

<br>

But first, we nap.

<br>

<img src="https://media.giphy.com/media/3o6fJ5LANL0x31R1Ic/giphy.gif" style="margin-left: 25%; border-radius: 10px; border: 10px solid pink">
 
 
 

 
 


