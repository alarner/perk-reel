# Setting up an API

> 01 Intro

## Greeting

Hi there. I'm really excited for our video today. It's going to be a fun one.

## Review

In the last video we learned how to create database tables using knex migrations.

## Introduction

Today we're going to continue along that path and write some back-end code to set up a RESTful API that will allow us to do basic create, cread, update and delete operations on out database. This will give us the power to store persistent data from the front-end of our application in our postgres database. This is a two step process. The first step is to create backend models that allow us to easily interact with the database tables that we created last time. The second step is to use some pre-built middleware to set up an API on top of those models.

> Sublime

## Walkthrough

In the directory structure that Perk gave us when we initially set up our project there is already a models directory. There are two files in here already, a User model and Authentication model. These models match up with the pre-defined create_users and create_authentication migrations.

> models/User.js

If we peek in the User.js file we can get a sense of what these models are going to look like. Models are defined using a node library that's built on top of knex, called bookshelf, and have thee important parts.

* First, they have a name. By convention models are singular, while database tables are plural. A table will hold many users, but a model represents one single user.
* Second, models define the database table that they should be connected with.
* Finally, they specify any important timestamp columns within the connected table.

We'll go over each of these pieces in detail.

> models/Link.js

Let's try this out on our own. I'm going to create a new file in the models directory called Link.js. I'm keeping it singular out of convention. Inside of this file I'm going to use bookshelf to to create a new model. We're going to learn more about the module.exports piece in a future video. For now just know that it needs to be there. The second argument of the bookshelf.model method is an options object. This object will always have a tableName property. In this case the table that we created in the last video with our migration script was called links. We're also going to specify any important timestamps that our table will store. This will usually be `createdAt`, `updatedAt` and `deletedAt`. These timestamps will automatically populated by our API. The `createdAt`, `updatedAt` and `deletedAt` timestamps have special meaning, so if you add other timestamps here, they will be ignored.

Let's do the same for our Image model as well. First I'll create the file, and then I'll fill in the model name, the table name, and the important timestamps.

Perfect! With just these few lines of code we're on our way to implementing a RESTful API. The final step is to use a piece of middleware to handle requests to the API. You can think of middleware kind of like a plugin for express, although the concept of middleware is quite a bit simpler and more elegant than a traditional plugin system yet still extemely and powerful. We'll learn more about how to write our own middleware in a a future video.

> Terminal

For now we're going to use a piece of pre-build middleware called bookshelf-api. Just to review, bookshelf is a library that makes it very simple to interact with our database tables. Bookshelf is an Object-relational mapping library, or ORM like you may find in other languages. For example Active Record in Ruby on Rails and SQLAlchemy in Python are both examples of ORMs. We're about to install a piece of middleware, which allows us to easily add functionality to our express application. We're going to use npm to install the middleware. Sorry for all the terminology! When we actually do this it will be more clear. It's important that I'm inside of my six-degrees project direction when I type the following command:

```
npm install --save bookshelf-api
```

This npm command is slightly different than what we've seen in the past. So far we've seen npm install -g to install a command line tool globally and we've seen plain old npm install to install all of the dependencies in a projects package.json file. What we're doing here is we are installing the bookshelf-api library locally in our six-degrees project and also saving it as a dependency in out packagel.json file.

> package.json

After running this command we can peek at our package.json file and see that its name and version are now listed as dependencies of this project. Now when any other developer downloads our code and runs npm install, they will get the bookshelf-api module in addition to all of the other project dependencies.

> app.js

I'm going to open up a new file that we haven't touched before. app.js in our project root is where all the magic starts. app.js is an express file that sets up and starts running our server. It's the file that first gets called when we run the `npm run dev` command to boot up our webserver.

Now I'll scroll down to the section labeled routes. Here's where I'm going to pull in the bookshelf-api middleware that I just installed using the CommonJS format for including modules. bookshelfApi is a function that will build the middleware that I want. All I need to do is pass it some options, specifically telling it where it can find our bookshelf models. I'm going to create apiMiddleware which will be the result of running out bookshelfApi function with an object that contains the path to our models directory.

Finally we're going to use this middleware. app.use is how we do that and we can specify which urls should use this middleware. I'm going to say anything that starts with /api/v1 should use the api middleware.

If you're still with me that's fantastic. If you're confused, that's okay too. We actually just wrote some really powerful code. We're going to keep working with this API so you'll have lots of time fill in your understanding of how it works. The bottom line is we now have an API. Don't believe me? I'll prove it to you.

I'm going to use postman, which is chrome based REST client, to make some requests to our API. There's a link in the resources section where you can install postman. First I'm going to make a GET request to localhost:3000/api/v1/image. Okay, we get back an empty JSON array. What if we make a post request? I'm going to fill in the originalFilename field as well as the original URL. Cool, we got back a response that included the id of the newly created image record on our server. Let's add a different one...

Our id is incrementing like we told it to in our migration!

Now if we make a GET request we'll see both images. We can also make a delete request, specifying the id of the image that we want to delete in the URL. Now we can see that record has been deleted.

Let's take a look at our images table in our database using PSequel. Notice that both records are still there, but the one that we deleted has a deletedAt timestamp listed. This is called a soft-delete. That record won't appear in our API but it still exists in the database so we can run amalytics on it or restore it if we ever need to. Bookshelf-api allows us to hard delete records too, meaning actually delete them from our database. It has a whole slew of other features like being able to filter, limit and sort records in our get requests, as well as update records as well. There's a link in the resources section to the bookshelf-api documentation, which lists out all of the features with examples of how to use them. We'll also learn in future videos how to secure this API so that anyone with postman can't just write any data they want willy nilly.

## Summary & Notes

### What did we do this time?

This is really cool. In the last few minutes we set up a simple RESTful API, which we'll use to store data within our application. We did this by setting up some bare bones models that match up with the database tables, which we created in the previous video. Then we used the bookshelf-api express middleware to process GET, POST and DELETE requests.

### Is there any homework?

If you want to get some more practice, one thing you can try before next time is to change the url prefix of our api from /api/v1 to something else of your choosing. I bet you can figure out how to do that. You can also try using postman to make API requests to the user, authentication, and link models.

### What is coming up next time?

In the next video we're going to transition over to the front-end. Perk has some great built in features for writing out front-end code like ES6 transpilation, Sass pre-processing and module loading using webpack or browserify. Next time we'll learn how to use some of these awesome features.

### What resources should they check out?

The code changes that we made in this video are all up on GitHub. Check them out through the link in the resources section

### Reminder about questions

and feel free to post any questions you have!
