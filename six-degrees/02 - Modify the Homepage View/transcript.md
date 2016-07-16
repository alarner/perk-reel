# Modifying the Homepage View

> 01 Intro

## Greeting

Hey there, welcome back. This is the second video in this video tutorial on creating a web application with node and express.

## Review

Last time we learned how to use a couple of command line tools to install perk, create a database to hold our data, bootstrap our project files and install all of the dependencies.

> Terminal

I wanted to quickly review the `npm` command, which you're going to be using very often as a node developer. If you remember, `npm` stands for node package manager. It allows us to install command line tools as well as third party libraries that we can use within our node applications. We learned about two different ways of using the `npm` command.

`npm install -g` followed by the name of a package will install that package globally.

`npm install` by itself will look inside of the package.json file within your current working directory to find all the dependencies of your project and install them.

In future videos we're going to learn about other ways of using `npm`. One interesting fact is that npm is the largest repository of packages on the planet, clocking in at over 300,000 as of this video. That's one of the most incredible things about node and JavaScript. There's such an incredible open source community and so many different modules to choose from. This can also be overwhelming at times, but Perk has chosen some of the best packages out there for us to start with. You can search through all of those packages at npmjs.com, which I've linked to in the resources section.


## Introduction

In this video we're going to learn how to modify the home page and also explore the perk configuration system.

> Sublime

## Walkthrough

First let's upen up the six-degrees directory that we created last time. I'm using Sublime Text, but you can use any editor that you like. There are a lot of files and directories here, but don't be overwhelmed, we're going to tackle each of the major pieces of this directory structure in pieces. In this video I want to talk about the views directory and the config directory. Let's take a look at the views directory first. This is where all of the HTML markup that gets rendered by our node app lives. Notice there are already a few files created for us including index, error and dashboard. There's also this auth directory where our default login and registration pages live. Today I want to tweak the home page. Let's open up index.html and take a look.

> views/index.html

This looks like a pretty standard html file. You might remember that this content was what appeared on our home page when we booted up our dev server last time.

> Terminal

Let's go ahead and start our dev server again if it's not already running. I'm going to use the `npm run dev` command to do that. Once it says that the server is running at localhost:3000 I'll open up that page in my browser.

> localhost:300

Looks just like last time.

> views/index.html

Let's try modifying that index.html view that we were just looking at. I'm going to change the heading to say Six Degrees and put in some filler text in a paragraph below.

> Terminal

If we look back to our terminal you'll notice that we get a message that says Server restarted from file change. Each time we change a file our server will reboot so that we can see that change reflected. I've used some node frameworks that are really slow and can take 5 to 10 seconds before you can actually see your change. That's super frustrating. Since my goal with Perk is to make development enjoyable I did a bunch of testing of different tools and picked the best to make sure that changes are reflected as quickly as possible.

> localhost:300

Alright, let's take a look at our browser and refresh the page. As you can see our change is up there. Pretty simple.

> views/index.html

One thing you may have noticed in the index view is that there was some non-standard syntax that doesn't look like HTML up at the top inside of the link and below in the script tag. Perk is set up by default to use the ejs templating engine. These angled brackets with percent signs allow us to inject dynamic content from the server into our views before they are rendered. Not everyone likes ejs though, so Perk is flexible and will allow you to use one of over 30 different templating engines. There's a link in the resources section on how to modify the templating engine that is used within your app.

This is a good time to talk about configuring and customizing our app. Remember how we typed in our database connection information and session secret the first time we ran the `npm run dev` command? Well this information is stored in a file called `local.js` inside of the config directory. The config directory stores all of the configuration information related to our project. Most of the files in this directory are default values for each of the configuration options in perk. For example `auth.js`, `build.js`, `database.js`, etc. The two files that start with the word local are special. `local.js` holds all of the configuration information specific to our local machine. It doesn't get checked in to git. `local.template.js` specifies which information developers should fill in when they first boot up our app. You can customize this template to ask for additional configuration info. Perk has a very robust configuration system that also supports environment specific overrides to your config info as well. If you're interested in learning more about the configuration system you should check out the configuration documentation, which is linked in the resources below this video. For now the important thing to remember is that if you ever want to modify the database connection information or session secret that we filled in last time, you can simply modify the `local.js` file.

> 02 Summary

## Summary & Notes

### What did we do this time?

In this video we learned how to modify our apps home page and other views. We also got a peek at the perk configuration system.

### What is coming up next time?

In the next video we're going to re-visit the database that we created in the first video and learn how to add database tables to our database using migrations.

### What resources should they check out?

* In the mean time feel free to check out some of many node modules that are available through npm.
* Specifically you might want to check out passport, express, redis and knex. These are the four pillars of perk that make up its name.
* The changes that we made to our project are all up on GitHub and linked in the resources as well.

### Reminder about questions

* Just like last time, if you have any questions or ran into any snags while following along, feel free to ask away in the questions section below. I'll answer them as quickly as possible.

See you next time!