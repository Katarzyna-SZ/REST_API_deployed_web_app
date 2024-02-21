# API testing in POSTMAN 📫🔥⚙️

#### Table of contents:
1. [About the project. Fundamentals of API testing in Postman](#subtask1)
2. [What are we going to test? Our web app deployment](#subtask2)
3. [Knowledge applied. E2E tests:](#subtask3)  
   - [Scope of work](#punkt1)
   - [Variables](#punkt2) 
   - [User autorization](#punkt3)
   - [Test scripts - examples](#punkt4)
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
***

### <a name='subtask3'>🚀 Knowledge applied. E2E tests</a>

First, we have to deploy the app on the Glitch service. The app's code is provided in a previously prepared repository. I create a unique application name with a unique URL address that serves only my testing purposes. Okay, let's start working.

<a name='punkt1'>**📌 Scope of work**</a>

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

<a name='punkt2'>**📌 Variables**</a>
- Creating enviroment variable for my URL base.
- Setting collection variables for the user TU1 (example):
```js
let jsonData = pm.response.json();

let userTU1Id = jsonData.id;
let userTU1Email = jsonData.email;
let userTU1Password = jsonData.password;

pm.collectionVariables.set("userTU1Id", userTU1Id);
pm.collectionVariables.set("userTU1Email", userTU1Email);
pm.collectionVariables.set("userTU1Password", userTU1Password);
```
- Setting collection variable for the article TA1 (example):
```js
let jsonData = pm.response.json();
let articleTA1Id = jsonData.id;
pm.collectionVariables.set("articleTA1Id", articleTA1Id);
```
- Settin collection variable for the comment TC1 (example)
```js
let jsonData = pm.response.json();
let commentTC1Id = jsonData.id;
pm.collectionVariables.set("commentTC1Id", commentTC1Id);
```
- Using Postman built-in variables such as:
```json
 {
    "firstname": "TU1 {{$randomFirstName}}",
    "lastname": "TU1 {{$randomLastName}}",
    "email": "TU1_{{$randomExampleEmail}}.{{timestampMS}}"
}
```
<a name='punkt3'>**📌 User autorization**</a>

Applying previously set variables for authorization purposes. Some functionalities require user authorization. By filling in all the required data (or in this case appropriate collection variables) using Basic Auth authorization, we are able to perform the required requests and tests of other functionalities to which the user is authorized like for exemple adding a comment etc.

<a name='punkt4'>**📌 Test scripts - examples**</a>

- **Checking status code for POST**
```js
pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);
});
```
- **Checking status code for GET, PUT, PATCH and DELETE**
```js
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
- **Checking if response body contains information that is required (examples)**
```js
let userTU1Id = pm.collectionVariables.get("userTU1Id");
pm.test("Body contains user TU1 id", function () {
    var textData = pm.response.text();
    pm.expect(textData).to.include(`"id": ${userTU1Id}`);
});

let articleTA1Id = pm.collectionVariables.get("articleTA1Id");
pm.test("Body contains article TA1 id", function () {
    var textData = pm.response.text();
    pm.expect(textData).to.include(`"id": ${articleTA1Id}`);
});

let commentTC1Id = pm.collectionVariables.get("commentTC1Id");
pm.test("Body contains comment TC1 id", function () {
    var textData = pm.response.text();
    pm.expect(textData).to.include(`"id": ${commentTC1Id}`);
});
```
<a name='punkt5'>**📌 POSTMAN Runner test results and THE collection**</a>
![E2E](https://github.com/Katarzyna-SZ/REST_API_deployed_web_app/assets/140599598/d828cfc4-d17c-4c8f-8538-ca7a76340f27)
***
<p align="center"><b>🙌🏻 RUN RESULTS</b></p>
<p align="center">[Here is my collection file with results. Enjoy!]()</p>



















