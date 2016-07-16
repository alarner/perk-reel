# Database Migrations - Creating Tables

> 01 Intro

## Greeting

Hello, welcome to the third video in our video series on how to create a LinkedIn clone using postgres and express.

## Review

If you remember last time we learned how to modify views within our application as well as how to update our database credentials and configuration.

## Introduction

Most modern web applications store persistent information. Relational databases are one way of storing that information. In this video we're going to learn how to modify the structure of our database using migrations. Relational databases like postgres use a table based structure to store data, kind of like an excel spreadsheet. Migrations allow us to create and modify the structure of tables in our database.

> Sublime

## Walkthrough

If we take a look at our six-degrees directory structure you can see that there's a migrations directory. We can write our migrations using the JavaScript syntax we already know and love.

You might have noticed that the migrations directory already has two files in it. That's because perk already has a nice user authentication system out of the box. This allows users to register and log in with their accounts. These migrations describe the table structure of the default user and authentication tables, which are used for registration and login.

So what tables other than users and authentication will we need for the Six Degrees project?

> 02 Database Schema

I've put together a database diagram that maps out all of the database tables that we're going to use. It looks pretty complicated but we're going to tackle it in pieces. We're not just building a trivial todo list here, so it's going to benefit us to think about the database architecutre of our app upfront. On the plus side, you're going to get a really good picture of the full power of perk by building something other than a simple toy app. I've added a link to this diagram in the resources section below the video.

> 03 Users, Links, Images Schema

In this video I want to focus on only two of these tables. If we learn how to build migrations for the links and images tables we will know most of what we need to build out the rest of the tables as well. We can apply the same patterns we learn with these two tables to the rest of our database.

If you're not familiar with entity relation diagrams like this one that's okay. The important things to know are that each main box represents what will eventually be one table in our database. On the right side of each box you'll see the column names, sometimes called fields, that will exist in that table. Certain columns will relate to columns in other tables. For example, the userId in the links table will point to an id in our users table. Columns like `userId` that reference another table are called foreign keys. You can easily pick out foreign keys because they have the letters FK to their left. They also have an arrow pointing to the table that they reference.

The last thing I'd like to point out is the bold text with the letters PK to their left. These are called primary keys, hence PK, and are usually a number that uniquely defines a record in the table where they live.

Ok enough database jargon. Let's build out these tables using migrations.

> Terminal

Knex is a fantastic full featured and stable node database connection library. It also represents the k at the end of Perk. We're going to use the command `knex migrate:make` to make a new migration. It's important that we are inside of the six-degrees directory when we do this. In this case I'm going to call the migration `create_links` because it will create our links table. Let's also make another migration called `create_images` by running the command `knex migrate:make create_images`.

> Sublime

What we've just done is create two new files. Knex put these files in our migrations directory. You can see them here and notice that they are all timestamped like the user and authentication migrations. The timestamps are important because they ensure that that the migrations will run in the correct order. For example, we wouldn't want our create_links migration to run before the users migration because then our links table would be referencing the users table which hasn't been created yet and postgres would error out. This is why it's important to use the `knex migrate:make command` instead of creating these files on your own.

> create_links

Let's open up our create_links migration. You'll see that there are two sections to this file: an exports.up and an exports.down. Inside of the exports.up function we are going to write all of the code to create our links table. The exports.down function will describe how to undo the changes that we made in exports.up, just in-case we need to rollback our database change in a hurry. Both exports.up and exports.down will always return a promise so that the knex migration tool will know when they are complete.

Inside of the exports.up function I'm going to return the result of knex.schema.createTable('links'), which takes a callback function. The callback function gives us a reference to the table that is about to be created, so that we can customize it. Based on our diagram we want to add eight columns to this table, id, createdAt, updatedAt, deletedAt, label, url, order and userId. There are several methods on our table reference that we can use to add a new column depending on its type.

The id is a special column. We want it to always increase its value by one so that we never have two rows with the same id. To do this we will use the increments method. We only want positive ids, so we will add the unsigned modifier as well as the primary modifier to denote that this is the primary key of this table.

`createdAt`, `updatedAt` and `deletedAt` will all be dates, so I'll use the datetime method and pass in the name of the column that I want to create. The `createdAt` date should always be filled in, but a record may have never been updated or deleted. updatedAt and deletedAt will be nullable, while createdAt will be notNull.

The label and url columns will both be strings and should not be null.

Order and userId will both be integers and neither of them should be null.

UserId is an interesting column because it's a foreign key. It references the users table. We can actually form that link by adding the references modifier, which we will pass the name of the column that the userId references. The name of the column alone isn't enough though because two tables could both have id columns. We need to also use the inTable modifier to specify which table this userId column points to. Finally we will add the onDelete('CASCADE') modifier to tell our database table what to do if the user that this link belongs to gets deleted. CASCADE will cause this record to be deleted if the owning user is deleted.

Luckily the exports.down function is much simpler. All we need to do is undo what we did in the exports.up. We are going to return knex.schema.dropTable('links'), which will delete the links table that was created in exports.up. exports.down will only ever be run if we make a mistake and need to undo this migration. This all looks good to me so I doubt we will ever need it, but better safe than sorry.

That was a bunch of stuff we just learned. Let's practice it once more on the create_images migration. I'm going to move through this quickly this time, but feel free to pause the video if you want time to follow along.

> create_images

Just like with links, we are going to create the table, this time called images, and add id, createdAt, updatedAt and deletedAt columns, all with the same types and modifiers as we used in the links table. We will also want originalFileName, original, medium and small columns, which will be strings and store information related to images that users upload for their profile. Finally we can drop the images table in our exports.down function. Alright! That wasn't so bad the second time.

> Terminal

Okay, how do we know if we did this correctly? Let's run those migrations! After all, these files just describe instructions for how to modify our database. If we want to actually run them we need to use the `knex migrate:latest` command. This command will run any migrations that haven't already been run, and get your database schema up to date. It's important that we are inside of the six-degrees directory when we do this. If everything works you'll see text describing which migrations were run.

> PSequel webpage

If we want to see a visual representation of our database now that our migrations have run, we can use a tool like PSequel. It's really nice and free. There's a link in the resources section so that you can download it.

> PSequel app

After downloading PSequel and opening it up you can fill in your database credentials. If you don't remember them you can find them in your config/local.js file. Notice you can see that we have users, authentications, links and images! If you click on any of them you can see the columns that we created in our migrations.

> 04 Summary

## Summary & Notes

### What did we do this time?

* Nice job getting through all of that. In this video we learned about entity relation diagrams and how to read and understand them.
* We used the entity relation diagram that's linked in the resources section and the `knex migrate:make command` to create migrations for two database tables.
* Finally we ran those migrations to set up those database tables within our database.

### Is there any homework?

* If you're feeling ambitious you can try and create migrations for some of the other database tables in the diagram.

### What is coming up next time?

* In the next video we're going to learn how to set up an API to allow us to perform basic create, read, update and delete operations on those fancy new database tables.

### What resources should they check out?

* I've added a link to the knex documentation in the resource below so that you can check out all of the different ways you can use knex to modify your database.

### Reminder about questions

As always, I look forward to your questions in the questions section below.