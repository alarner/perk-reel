# Up and Running

> 01 Intro

## Greeting

Hi. Thanks for taking the time to check out this video tutorial on creating a web application with node and express. My name is Aaron Larner. I'm one of the developers behind the node framework, Perk. Throughout the course of this video series we're going to be building and deploying a full fledged node application. This tutorial is designed for those who have previous programming experience and want to expand that knowledge to include nodejs.

Before we begin I wanted to point out that there are two helpful sections below this video. First is a resources section where I'll provide links to any information and tools that I cover in the video, as well as a link to GitHub where you can view the code that we wrote. Below that is a questions section. If you run into any questions throughout the course of this video feel free to ask questions and I will answer them as fast as I possibly can.

## Introduction

You're might be curious about what were going to build and how to get your project set up. Getting up and running with node can be difficult and time consuming if you've never done it before.

In this video I'm going to give you an overview of the project that we're about to create as well as help you quickly get through that set-up work so that you can get to the fun stuff faster.

> 02 Install Node, Redis, Postgres

I'm going to assume you already have node, postgres and redis installed. If you don't have those tools installed yet, there's a great guide on how to do that within the Perk documentation, which I've linked to in the resources section below. Feel free to hit pause, install those tools and then come back. I'll be here patiently waiting. You can post any of your installation related questions below.

> 03 Home

## Walkthrough

Whenever I start a new project I like to get a good visual picture of what i'm going to be building. In this video series we're going to be building a LinkedIn clone called Six Degrees. I chose a LinkedIn clone for two reasons. Most importantly this is not a trivial project like a todo list or blog. It will give you a really good picture of what it's like to develop with Perk. Secondly, I think the user experience of LinkedIn is terrible so why not try to do it better? I've put together a few wireframes that outline the functionality that our app will include.

### Home Page

Six Degrees will have a pretty standard home page that explains what the application is and allows you to register or log in.

> 04 Dashboard

### Dashboard

After logging in you'll be taken to a search page where you can find new professionals to connect with, either by browsing or searching.

> 05 View Profile

### View Profile

After clicking on a persons name or picture you'll be taken to their profile, where you can see information about their work history as well as external links they've shared like Twitter, GitHub, etc. You'll also be able to request to connect with them.

> 06 Edit Profile

### Edit Profile

You'll also be able to edit your own profile, filling in information about your professional accomplishments.

> 07 Messages

### Messages

Finally, you'll be able to exchange messages with your connections.

I've linked to these wireframes in the resources section below if you want to check them out in more detail.

> Terminal

## Setup

Now that we've got an idea of what we're about to build, let's get our initial file structure set up and our basic webserver running. To do that we're going to use Perk. If you don't know anything about Perk, it will help us set up a bunch of our boilerplate code. Don't worry, we're going to learn about each of the major directories that it creates over the course of this video series. To install perk we're going to use `npm`, which is the node package manager. If you've already installed node then you will also have npm installed. npm allows us to install third party command line tools as well node libraries that we can use within our application. To install perk type:

```
npm install -g perk-cli
```

perk-cli is the perk command line tool. The -g instructs npm to install this command globally. Without the -g the perk-cli will only be installed within our current working directory. You can make sure that the installation was successful by typing `perk` into your terminal. You should see instructions for how to use the command.

These instructions tell us to provide an install path where we want our new application to live, so I'm going to type:

```
perk six-degrees
```

This downloads the perk boilerplate files from GitHub and unzips them in a new directory named six-degrees. We're going to cd into that new directory and use the `npm install` command again. This time instead of specifying a specific library to install we're just going to type `npm install`. This is going to look inside of a file called package.json for all of the dependencies of this project and install them. This might take a little bit, I'm going to speed it up but feel free to pause and wait for your install to finish.

Great! Now that that's finished we're going to create a database that will eventually house all of the data for Six Degrees. If you have postgres installed you can use the `createdb` command followed by the name of the database that you'd like to create. I'm going to call the database six-degrees.

```
createdb six-degrees
```

Alright! We're almost there! To boot up our development server let's run the command:

```
npm run dev
```

This will boot up our webserver, compile frontend JavaScript assets using webpack and babel and process Sass files.

Since this is the first time we've run this command it's going to ask us for a little bit of information, specifically how to connect to the database that we just created and for a random session secret to encrypt our user sessions. Perk is focused on optimizing for developer hapiness, so this is one of those little things that makes your life nicer because you don't have to hunt for config files. In a future video I'm going to show you how to customize this screen in case your application requires other config information that needs to be specified before you can run it.

We're using postgres so our client will be "pg". You can use enter or the up and down arrow keys to move between fields. The host will be localhost. The user will be the username that you use to log in with your computer. Likely you won't have a password so you can type in ctrl+r to remove that field. We named our database six-degrees. Finally let's type in a random string to sncrypt our sessions. ctrl+s will save this configuration so that the next time we use the `npm run dev` command we won't have to fill out this information again.

Great! If everything worked you'll see that sass compiled our basic Sass file, webpack bundled our javascript files and our webserver is runing at localhost:3000. Let's go to localhost:3000 in our browser and see what happens. If you see this basic home page you've done it correctly! Nice job!

The last thing I want to show you is how to shut down your webserver. It's pretty simple, you just type ctrl+c to exit out.

> 08 Summary

## Summary & Notes

### What did we do this time?

* In this video you accomplished a lot!
* We ran through an overview of the functionality that we want for our LinkedIn clone.
* We learned a little bit about npm and how to install third party node libraries and command line tools and installed the perk command line tool.
* We created a database for our app and set up our basic project.
* Finally, we learned how to boot up and shut down our development server .

### What is coming up next time?
* In the next video we're going to learn a little bit more about the configuration system in case you need to change your database connection credentials or session secret.
* We're also going to learn about basic views and how to modify our home page.

### Reminder about questions
* Lastly I wanted to remind you about the resources and questions sections below this video. If you have any questions about the stuff that we covered in this video I'd love to answer them. 
* All of the code that we set up in this video is on GitHub and linked to in the resources section below as well as links on how to set up node, postgres and redis and the Six Degrees wireframes.