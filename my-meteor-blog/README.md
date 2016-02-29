
To make and start meteor app:

meteor create simple-todos
cd simple-todos
meteor

> REMEMBER: TO MAKE SERVER: REFER TO CHAPTER 3 AND 4 OF SINGLE PAGE APP WITH METEOR BOOK AND 
AND CODE IN ALL CODE


** I probably need to make post, get, delete, update (REST) commands to finish the app, 
as well as change appearance a little
Add a button to one of these pages and post data with it
**

1) Dont need to add anything to server

2)Index page with nothing

3)routes.js with router

4)Layout.html page with yield and links	and template (in html page)

Link:
	<li>
		<a href="/">Home</a>
	</li>
	
Yield:
	<main> 
	{{> yield}}
	</main>
so that routes can be added dynamically

Template in HTML page: 
<template name="newpage">

5) To add events  can use button <button>Get some random number</button> then reference event in js file.
	{{> contextExample dataContextHelper}}

	{{#with dataContextHelper}}
		{{> contextExample}}
	{{/with}}

// Adding events
Template.contextExample.events({
	'click button': function(e, template){
		Session.set('randomNumber', Math.random(0,99));
	}
});

6) SERVER:

1. Main.js
 *  THIS SIMPLE DISPLAYS THE INFORMATION THAT WILL BE ADDED TO THE SERVER ON STARTUP IF THE DATA IS NOT THERE ALREADY

2. Collections.js

// #Storing Data -> Setup a collection
Posts = new Mongo.Collection('posts');

3. Publications.js
- lazy loads posts onto client side:
// #Controlling the data flow -> Lazy load posts or how to change subscriptions
Meteor.publish('lazyload-posts', function (limit) {
	return Posts.find({}, {
		limit: limit,
		fields: {
			text: 0
		},
		sort: {timeCreated: -1}
	});
});

-POSTS DATA AND returns posts
// #Routes -> Setting up the post route
Meteor.publish("single-post", function (slug) {
	return Posts.find({slug: slug});
});


