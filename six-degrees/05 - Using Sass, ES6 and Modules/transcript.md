# Using Sass, ES6, and Modules
> 01 Intro

## Greeting

Alright, video five. We're really starting to get into the swing of things here.

## Review

In the last four videos we learned how to set up our project, create a database and database tables using migrations. Finally, we learned how to use middleware to set up a RESTful API.

## Introduction

In this video were going to temporarily switch gears and talk about the front-end. Perk has a bunch of really useful out of the box features to make your life on the front-end enjoyable. In this video we're going to learn about how Perk compiles your front-end assets including, JavaScript modules, ES6 and Sass.

> localhost:3000

## Walkthrough

This is going to be a fairly short video because luckily there's not much prep work we need to do, we can just start writing code from the get-go. If you recall, our current home page looks like this.

> Sublime

Let's go ahead and modify that header to use a new font and color. All of my front-end code lives in the public directory. My sass files are in public/styles, and my Sass entry point is main.scss. Let's go into main.scss and modify our h1 element to have a color #333 and a font-family of Open Sans with a fallback to sans-serif. Great, I'm also going to give it a hover state color of #999. Here I'm using sass nesting and the & notation for referencing a parent selector. This is not native CSS functionality, but it will be pre-processed using Sass.

> localhost:3000

If we check back in our browser and refresh the page you can see that our heading changes and has a new hover state as well. It's that simple. All features of Sass will work right out of the box.

> Sublime

Let's write a little bit of front-end javascript next. Inside of public/scripts I have a main.js file, which is my JavaScript entry point. Here I'm going to add a little message if you click on the header, just for the sake of example. First I'll use an ES6 const to grab a reference to my h1 element. Next I'll add an event listener to this element using an arrow function as a callback, which will call alert. Behind the scenes Perk uses Babel to transpile this ES6 code to ES5 so that it's supported in all browsers.

> localhost:3000

Back in the browser we can see that the JavaScript that we just wrote is working.

> Sublime

The last thing I want to talk about today is CommonJS and ES6 style modules. You've actually seen CommonJS modules in some of the previous videos, but I didn't explicitly call them out. As developers we like to be able to break out our code into re-usable chunks so that we don't have to repeat ourselves if we're performing the same task over and over. Often it's really handy to keep each logical chunk of code in a different file. CommonJS modules allow us to do this. This has always been supported in Node, but has just been introduced to front-end JavaScript with ES6. I'm going to show you an example of sharing code between files on the front-end. First I'm going to create a new file called alert.js. In here I'm going to write a function called showMessage that alerts a new message. In order to share this code with other files we need to export it. With CommonJS you can export any variable, expression or function. In this case I'll export the function by assigning module.exports equal to the function itsself.

Using this code is now simple. Inside of my main.js I can create a new variable called showMessage and import my showMessage code using the require statement by passing in the path to that file. Whatever got exported from that file is the value that showMessage inside of my main.js file will assume.

We can change our alert here to call the showMessage function that we imported. Let's check it out in the browser.

> localhost:3000

Let's refresh the page first. Works like a charm.

> Sublime

The way that modules work on the front-end is by using a tool like webpack or browserify. Perk supports both webpack and browserify, and you can configure which tool you'd like to use my modifying the build.js file inside of the script directory. I find that webpack is better for development because it's super fast, but browserify is better in production because it produces smaller compiled files.

The last thing I want to mention about modules is that if you prefer the ES6 module syntax using import and export that is also supported on the front-end, however it is not supported on the backend. All of your node code must use CommonJS.

## Summary & Notes

### What did we do this time?

In this video we learned about three of the out of the box features that you can use with Perk in your front-end code. Those features are Sass pre-processing, ES6 to ES5 transpilation using Babel and JavaScript modules using either Webpack or Browserify.

### What is coming up next time?

Next time we're going to continue with the front-end by setting up our single page app structure with React and React Router.

### What resources should they check out? / Reminder about questions

In the resources below I've included the code we wrote today as well as links to the Sass documentation and some solid tutorials for CommonJS and ES6 Modules.
