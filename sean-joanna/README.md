![CF](https://camo.githubusercontent.com/70edab54bba80edb7493cad3135e9606781cbb6b/687474703a2f2f692e696d6775722e636f6d2f377635415363382e706e67) Lab 08: SQL and PostgreSQL
===

## Code Wars Challenge

Complete [today's Kata](https://www.codewars.com/kata/format-words-into-a-sentence) and follow the submission instructions from Lab 01.

## Lab 08 Submission Instructions
Follow the submission instructions from Lab 01.

## Resources  
[SQL Syntax Cheatsheet](cheatsheets/sql.md)

[PostgreSQL Shell Cheatsheet](cheatsheets/postgress-shell.md)

[PostgreSQL Docs](https://www.postgresql.org/docs/)

## Configuration
_Your repository must include:_

```
08-sql-intro-and-postgres
└── starter-code
└── driver-navigator
  ├── .eslintrc.json
  ├── .gitignore
  ├── LICENSE
  ├── README.md
  ├── node_modules
  ├── package-lock.json
  ├── package.json
  ├── public
  │   ├── data
  │   │   └── hackerIpsum.json
  │   ├── index.html
  │   ├── new.html
  │   ├── scripts
  │   │   ├── article.js
  │   │   └── articleView.js
  │   ├── styles
  │   │   ├── base.css
  │   │   ├── layout.css
  │   │   └── modules.css
  │   └── vendor
  │       ├── scripts
  │       │   └── highlight.pack.js
  │       └── styles
  │           ├── fonts
  │           │   ├── icomoon.eot
  │           │   ├── icomoon.svg
  │           │   ├── icomoon.ttf
  │           │   └── icomoon.woff
  │           ├── default.css
  │           ├── icons.css
  │           ├── normalize.css
  │           └── railscasts.css
  └── server.js
└── PULL_REQUEST_TEMPLATE.md
└── README.md
```
## Steps to Follow

Getting this lab up and running is all about following a sequence of steps, and it is also immportant to know what those individual steps do. Also take note of the documentation provided in the lab directory. It will be helpful.

**DO THESE STEPS IN ORDER. TAKE YOUR TIME. READ THE ERROR MESSAGES SO THAT WHEN YOU SEE THEM AGAIN YOU KNOW HOW TO DEBUG.**

1X. Do all of the usual forking and cloning and navigate into your copy of the `starter-code` directory in your terminal. This terminal tab/window will be for your access to the file system and for Git stuff. Go ahead and `code .` to get your editor open.
2X. Open your `server.js` file and set the proper value for your `constring` variable for your operating system and SQL setup. Also, pass in the `conString` as an argument where we instantiate a new Client.
3x. Back to the terminal: Make a copy of this terminal tab/window and be sure it is in the same directory where `server.js` is at the root level. This is where you will run your Node server. But not yet...
3x. Create ANOTHER terminal tab/window; the directory that this one is in does not matter. This is where you will open your SQL shell. Go ahead and run `psql` in this tab, and you should get your SQL shell prompt. Type in `\dt` and you should get back a "No relations" message.
4x. Now go back to the server tab and start the server. It should error, complaining that it cannot find the module `pg` (or it might complain about not finding express if you haven't already done a `npm i`, so do that and try again!). That is because we have not yet required `pg` into our server code nor have we installed it from NPM. So let's do those steps:
5x. In your server code, put `const pg = require('pg');` with your other variable declarations at the top.
6x. In your terminal, run `npm i --save pg` to load `pg` from NPM. Be sure to save the edits.
7x. Try running the server code again. It should work.
8x. Go to your SQL shell and `\dt` again. You should see the tables `articles` listed. Enter `SELECT COUNT(*) FROM articles;` and you should see that there are 250 records in the DB.
9x. Go to your browser and open `localhost:3000`. You should see the blog WITHOUT all of its articles. Dammit... now what? Something is wrong. Let's track it down.
10x. Oooohhhh.... trace the execution... `Article.fetchAll(articleView.initIndexPage);` is called in `index.html`... when we look in `article.fetchAll()` we see that it is doing a `$.get('/articles')`, so let's go look at that route in the server.
11x. ARGH THERE IS NO SQL IN THE `client.query()`!!! Let's fix that.
12x. In the empty quotes, enter `SELECT * FROM articles;` and save the file.
13x. Refresh the browser.
14x. Articles!!!!!!

OK, from here on, start working through all of the `COMMENT` items in the code.

Once you are done with that, finish the last two unfinished SQL queries. Sam will give those to you by 11:00 this morning if you have not got them yet. Try to write them on your own.

How will you know if they work, though?

Follow the steps in the `CRUD-testing.md` doc in the "cheatsheets" directory of the lab.

Play around with things and have fun. Try entering new articles in the form. Break things. Fix things. Get your fingers dirty with all of this and seek to understand how it all fits together.

Whee!!!!!!


## User Stories and Feature Tasks

*As a user, I want to store my articles in a database so that my articles are available for users from an external source.*

- Install and require the NPM PostgreSQL package `pg` in your server.js file.
- Make sure to complete the connection string.
  - Windows and Linux users: You should have retained the user/password from the pre-work for this course. Your OS may require that your connection string is composed of additional information including user and password. For example: `const conString = 'postgres://USER:PASSWORD@HOST:PORT/DBNAME'`;
  - Mac users: `const conString = 'postgres://localhost:5432'`;
- Pass the appropriate argument when instantiating a new Client.
- The articleView.js methods are different now that we are not accessing the JSON file directly, and instead retrieving the articles from a database. Therefore, we no longer need to export the JSON, so remove all code that was involved in performing this action.

*As a developer, I want to write proper SQL queries so that I can interact with the blog articles in my database.*

- Write a SQL query to retrieve all of the articles from your database.
- Write a SQL query to update a single article in your database. Make sure to provide the appropriate data for the article.
- Write a SQL query to remove all articles from your database.


*As a developer, I want to review my code base so that I have a deep understanding of its overall functionality.*

- Study each of the new routes in your server.js file by examining the SQL statements and any associated data being handed through the request.
- For each of the `COMMENT` items in server.js, provide a brief description of what that function immediately below is doing. Be sure to indicate, where applicable, details such as:
  - What number(s) of the full-stack-diagram.png image is this part of the code interacting with?
  - Which method of article.js is interacting with this particular piece of server.js?
  - What part of ***CRUD*** is being enacted/managed by this particular piece of code?
  - As applicable, an additional sentence or two of explanation about what the code is doing, what NPM packages are involved, etc. The goal is to demonstrate that you understand what is going on in the code without glossing over details, but also without writing a novel about it.

## Documentation
_Your README.md must include:_

```md
# Project Name

**Author**: Your Name Goes Here
**Version**: 1.0.0 (increment the patch/fix version number up if you make more commits past your first submission)

## Overview
<!-- Provide a high level overview of what this application is and why you are building it, beyond the fact that it's an assignment for a Code Fellows 301 class. (i.e. What's your problem domain?) -->

## Getting Started
<!-- What are the steps that a user must take in order to build this app on their own machine and get it running? -->

## Architecture
<!-- Provide a detailed description of the application design. What technologies (languages, libraries, etc) you're using, and any other relevant design information. -->

## Change Log
<!-- Use this are to document the iterative changes made to your application as each feature is successfully implemented. Use time stamps. Here's an examples:

01-01-2001 4:59pm - Application now has a fully-functional express server, with GET and POST routes for the book resource.

## Credits and Collaborations
<!-- Give credit (and a link) to other people or resources that helped you build this application. -->
-->
```
