# API testing in POSTMAN 📫🔥⚙️

#### Table of contents:
1. [About the project. Fundamentals of API testing in Postman](#subtask1)
2. [What are we going to test? Our web app deployment](#subtask2)
3. [Knowledge applied. E2E tests:](#subtask3)  
   - [Scope of work](#punkt1)
   - [Variables](#punkt2) 
   - [User autorization](#punkt3)
   - [Creating pre-scripts and scripts for tests - examples](#punkt4)
   - [POSTMAN Runner test results and THE collection](#punkt5)
<hr>

### <a name='subtask1'>🎯 About the project</a>

A project I am about to present is the result of applying the knowledge gained from the module on *API testing with the Postman tool*, part of the **REST API Manual and Automation Foundation Level** course organized by [Jaktestowac.pl](https://jaktestowac.pl/). 

🧠**What have I revised and learnt in the process?**

✔️HTTP protocole and response codes
✔️REST API methods: GET, POST, PUT, PATCH, DELETE.
✔️Work with API documentation on Swagger
✔️Test REST API with Chrome DevTools
✔️Create collections and different levels of variables
✔️Perform CRUD tests for various functionalities available in the app
✔️Test user Authentication and Authorization: Basic Auth, JWT and Bearer Auth
✔️Use Console in Postman to verify responses
✔️Write all the necessary pre-scripst and simple tests
✔️**Perform e2e test of deployed app**
***
### <a name='subtask2'>🔍 What are we going to test? Our web app deployment</a>

We are going to test a web application that has been temporarily named *Rest Api Demo* and consists of functionalities such as:
- user registration and login,
- creating and adding articles,
- editing articles,
- adding comments and their editing,
- deleting users, articles and comments

First, we have to deploy the app on the Glitch service. The app's code is provided in a previously prepared repository. I create a unique application name with a unique URL address that serves only my testing purposes. Okay, let's start working.

**📋 Scope of work**

**Seed** | 
--- |
POST Create new user TU1| 
POST Create new user TU2 |

|Users |Articles |Comments |Delete 
|:- |:- |:- |:-
|GET Get all users with TU1 and TU2 |POST Create article TA1 for user TU1 |POST Create comment TC1 for article TA1 and user TU1 |DELETE Delete comment TC3
|GET Get single user TU1 |PUT Create article TA2 via update with user TU2 |GET Get all comments with TC1 |DELETE Delete comment TC2
|GET Get single user TU2 |GET Get all articles with TA1 and TA2 |GET Get single comment TC1 |DELETE Delete comment TC1
|PUT Update existing user TU1 |GET Get articles (with params user id TU1) |PUT Update comment TC1 for article TA1 and user TU1 |DELETE Delete article TA2
|PUT Update existing user TU2 |PUT Update article TU1 |PATCH Update comment TC1 body (article TA1 and user TU1) |DELETE Delete article TA1
|PATCH Update user TU1 firstname |PATCH Update TA1 article's title |POST Create comment TC2 for article TA1 and user TU2 |DELETE Delete user TU2
| | |PUT Create comment TC3 via update for user TU2 |DELETE Delete user TU1















