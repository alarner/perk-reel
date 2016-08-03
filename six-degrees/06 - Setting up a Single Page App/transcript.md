# Setting up a Single Page App

> 01 Intro

## Greeting

Hey folks. Great job completing the first five videos in this video. That's an awesome accomplishment and we've already covered a lot of material.

## Review

In the last video we took a little detour from our LinkedIn clone project and learned how Perk handles front-end assets.

## Introduction

In this video we're going to continue working mostly on the front-end. We're going to set up the basic structure of our single page app, including a global navigation and some skeleton pages. For the six degrees front-end I'm going to be using React with React Router. If you've never used react before I've linked to some great React tutorials in the resources section below. I'd recommend getting a little bit familiar with React before continuing with this video.

> Terminal

## Walkthrough

Let's start by installing react, react-router and react-dom with npm. I'm going to use the --save flag to ensure that these packages are listed as dependencies in my package.json file. `npm install --save react react-dom react-router`

> main.js

Next I'm going to open up my main.js file inside of scripts. I'm going to clear out this demo code that we wrote last time. Here's where I'm going use React and React Router, so I'll start by requiring React, ReactDOM and finally a few different pieces from React Router. Here I'm using ES6 destructuring to pull out a few specific properties from the required react-router object. If ES6 destructuring is new to you, I've linked to an article that explains it in the resources section below.

Cool, next I'm going to create a new variable called `app` that is going to use the React router that we required above. What I'm writing here is JSX. It's an HTML-like syntax that allows us to easily construct React elements within our JavaScript code. Our Router element is going to take one property, history - which specifies the technique that we will use to keep track of our page history. I'm going to use browserHistory, which uses HTML5 push state to manage the history. You may also use hashHistory instead if you prefer to use hashes in the URL to manage the page history. If I were to use hashHistory instead of browserHistory I would need to include hashHistory up here instead of browserHistory.

> index.html

Alright, the next step is to actually inject this React element onto our page. Before we do that we need a place for it to get live, so I'm going to modify my homepage to have one empty div element with an id of app. This will act as a placeholder for our dynamilcally generated content controled by React.

> main.js

Back in our main.js file I'm going to use ReactDOM to render the app element into that placeholder element that we just created.

> localhost:3000

Let's take a look. Well, it's just a blank page because we haven't added any content yet, just an empty router. Let's start by creating our first React component to get some stuff on that page.

> App.js

Inside of my scripts directory I'm going to create a new new directory to house all of our React components. Inside of that new directory I'll create a new file called App.js. This file is going to contain all of the content that will be shared between all pages. In our case, our global navigation will live here.

I'm going to start by requiring React and the Link property from React Router. Then I'm going to export a new React component. I'm using the traditional React.createClass method here instead of the newer ES6 style classes because I prefer the old notation. At bare minimum each react component we create needs a render method so I'm going to create that. The render method returns the JSX markup that this component will display on the page. Here I'm going to include a basic navigation that has links for the home page, edit profile page, connections page and messages page. I'm also going to include regular anchor tags for the login and register pages. The difference between Link elements and anchor tags is that Link elements will use react router to switch the page without making a new HTTP request whereas the anchor tags will actually cause a new page request to be made. Finally, I'm going to add a place for our unique page content to live. I'll do this by injecting {this.props.children} where I want the unique page content to live. The curly braces let me inject javascript expressions into the JSX markup. Remember that the App component that we're creating here is just a skeleton component. It's going to have all of the shared content that will appear on every page, but the unique content for each page will live in it's own unique page component that will get placed where {this.props.children} appears.

> main.js

Okay, back in my main.js file I'm going to require my App.js file and create a new Route within my router. This route tells all pages to use the App.js component.

> localhost:3000

Looking back in our browser we can see that we now have our links showing up and if I click on these links it will change the URL. We're almost there. Just three more steps. What we have is a working skeleton but let's fill in some of the space, namely the content pages. I'm going to create a basic React component for each of the pages we'll need. Let's start with the home page.

> Home.js

I'm going to create a new directory inside of our components directory to house our specific page components. Then I'll create a new file called Home.js for our home page. Inside of the Home.js file I'm going to follow the same basic steps that we did for the App.js file. First I'm going to require React. Next I'm going to export a new React class. Each react component needs a render method so let's create one for our Home page. I'm going to keep it simple. Let's just put an h1 that says home inside of a section element. React render methods can only return one element, so I like to wrap every thing inside of one root element. Usually a section or a div. Perfect!

> Terminal

I'm going to quickly duplicate that Home component to create my EditProfile, Connections and Messages pages. Then I'll jump into those new files and just switch up the h1 content to reflect that particular page. Okay, two more steps. First let's add routes for each one of those new pages inside of our main.js file.

> main.js

To do this I'm going to require each one of those page components and then I'm going to add new Route elements inside of our App route. Nesting these routes inside of the App route is what will place them where we injected {this.props.children} earlier in the video. For each route I'll specify the path where that page should be displayed.

> localhost:3000

Let's check this out in the browser again. This time when we go to localhost:3000 we see our home page. If we click on the Edit Profile link we can see the url change and the content also changes. This is great progress! We're almost there, just one small last step. So we're on the edit profile page. Everything looks good, but what happens if we refresh the page? Yikes we get a 404. This is because when we refresh the page, our backend express router takes over and looks for a back-end route at the path of edit-profile and we don't have one of those. We only have one on the front-end. The solution is to add a fallback route that tells express to load our index.html view if the route it was looking for wasn't found. This will hand control over to the react router in our main.js file on the front-end. To do this I'm going to open up app.js.

> app.js

If you remember back to video 4 where we set up our API we also modified this file. I'm going to scroll down to the routes section. Notice below all of our routes we have a catch-all route that shows a 404 error if no route matched the one that the visitor has requested. Instead of showing a 404 I'm going to modify this catch-all route to render the index view. This way, when our edit-profile path doesn;t match one of the backend route, we will still render the home page, which will know to render the edit profile page on the front-end.

> localhost:3000/edit-profile

If we take one final look in the browser and refresh, we can see that the 404 error goes away and our edit profile page correctly displays. We can also switch back and forht between pages and refresh as we please. Everything works as intended.

## Summary & Notes

### What did we do this time?

We did a whole lot this time, so feel free to go back and re-watch parts of the video that didn't make sense. Also feel free to post questions in the questions section below. To recap, we installed react, react-dom and react-router to help organize our front-end code into components. We used react-router to create routes for our home, edit profile, message and connections page components. Finally, we fixed a 404 error that was preventing our pages from displaying when we refreshed the page. We now have a great structure for the front-end code that we'll write in the future.

### Is there any homework?

If you want to make some more progress before the next video I'd recommend learning about React from the tutorials in the resources section below. You can also try to modify the home page component to have some more interesting content, or maybe even style it with some custom CSS. This is all within your power with the tools that we've covered so far.

### What is coming up next time?

In the next video we're going to talk about the built in Perk authentication system and learn how to use it.

### What resources should they check out? / Reminder about questions

The code that we wrote in this video is up on GitHub. Check it out through the link in the resources section.
