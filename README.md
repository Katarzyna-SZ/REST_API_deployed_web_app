# API testing in POSTMAN 📫🔥⚙️

#### Table of contents:
1. [About the project. Fundamentals of API testing in Postman](#subtask1)
2. [What are we going to test? Our web app deployment](#subtask2)
3. [Knowledge applied. E2E tests:](#subtask3)  
   - [Scope of work](#punkt1)
   - [Variables](#punkt2) 
   - [User autorization](#punkt3)
   - [Test scripts - examples](#punkt4)
   - [POSTMAN Runner test results](#punkt5)
   - [Summary](#punkt6)
<hr>

### <a name='subtask1'>🎯 About the project</a>

This project showcases the application of knowledge gained from a module on *API testing with Postman*, part of the **REST API Manual and Automation Foundation Level** course organized by [Jaktestowac.pl](https://jaktestowac.pl/). 

🧠 **What I Revised and Learned:**

- Understanding of the HTTP protocol and response codes
- Familiarity with REST API methods: GET, POST, PUT, PATCH, DELETE
- How to work with API documentation on Swagger
- Testing REST APIs with Chrome DevTools
- Creation of collections and different levels of variables
- Execution of CRUD tests for various app functionalities
- Testing of user Authentication and Authorization: Basic Auth, JWT, and Bearer Auth
- Usage of the Postman Console to verify responses
- Writing necessary pre-scripts and simple tests
- **End-to-end (E2E) testing of the deployed app**
***
### <a name='subtask2'>🔍 What are we going to test? Our web app deployment</a>

We are going to test a web application that has been temporarily named *Rest Api Demo* and consists of functionalities such as:
- user registration and login,
- creating and adding articles,
- editing articles,
- adding comments and their editing,
- deleting users, articles and comments
  
![Articles](https://github.com/Katarzyna-SZ/REST_API_deployed_web_app/assets/140599598/b4d1fcc2-bc41-4a9e-a979-78df4cd92639) ![Users](https://github.com/Katarzyna-SZ/REST_API_deployed_web_app/assets/140599598/5de994f8-5cf8-41dd-b58c-b17a3674e8bc)

***

### <a name='subtask3'>🚀 Knowledge applied. E2E tests</a>

First, we have to deploy the app on the Glitch service. The app's code is provided in a previously prepared repository. I create a unique application name with a unique URL address that serves only my testing purposes. Okay, let's start working.

<a name='punkt1'>**📌 Scope of work**</a>

**Seed** | 
--- |
POST Create new Test User 1| 
POST Create new Test User 2|

|Users |Articles |Comments |Delete 
|:- |:- |:- |:-
|GET Get all users with Test User 1 and Test User 2 |POST Create article Test Article 1 for Test User 1 |POST Create Test Comment 1 for Test Article 1 and Test User 1 |DELETE Delete Test Comment 3
|GET Get single user Test User 1 |PUT Create Test Article 2 via update with Test User 2 |GET Get all comments with Test Comment 1 |DELETE Delete Test Comment 2
|GET Get single user Test User 2 |GET Get all articles with Test Article 1 and Test Article 2 |GET Get single Test Comment 1 |DELETE Delete Test Comment 1
|PUT Update existing Test User 1 |GET Get articles (with params user id Test User 1) |PUT Update Test Comment 1 for Test Article 1 and Test User 1 |DELETE Delete Test Article 2
|PUT Update existing Test User 2 |PUT Update Test Article 1 |PATCH Update Test Comment 1 body (Test Article 1 and Test User 1) |DELETE Delete Test Article 1
|PATCH Update user Test User 1 firstname |PATCH Update Test Article 1 article's title |POST Create Test Comment 2 for Test Article 1 and Test User 2 |DELETE Delete Test User 2
| | |PUT Create Test Comment 3 via update for Test User 2 |DELETE Delete Test User 1

<a name='punkt2'>**📌 Variables**</a>
- Creating enviroment variable for my URL base.
- Setting collection variables for Test User 1 (example):
```js
let jsonData = pm.response.json();

let userTU1Id = jsonData.id;
let userTU1Email = jsonData.email;
let userTU1Password = jsonData.password;

pm.collectionVariables.set("userTU1Id", userTU1Id);
pm.collectionVariables.set("userTU1Email", userTU1Email);
pm.collectionVariables.set("userTU1Password", userTU1Password);
```
- Setting collection variable for Test Article 1 (example):
```js
let jsonData = pm.response.json();
let articleTA1Id = jsonData.id;
pm.collectionVariables.set("articleTA1Id", articleTA1Id);
```
- Settin collection variable for Test Comment 1 (example)
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
- **Authorization Process:**
   - Applying previously set variables is crucial for user authorization. We ensure that all necessary data, including collection variables, is appropriately filled in to meet the authorization requirements. Utilizing Basic Auth, we facilitate the authorization process.
- **Execution of Authorized Functionalities:**
   - Once the authorization process is completed, we gain the ability to execute requests and tests on authorized functionalities. These functionalities are accessible to the user based on their authorization level.
- **Example Functionality:**
   - For instance, one such authorized functionality could involve adding a comment. By following the authorization process, users can seamlessly access and utilize various features within the system.

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
<a name='punkt5'>**📌 POSTMAN Runner test results of the test collection**</a>
![E2E](https://github.com/Katarzyna-SZ/REST_API_deployed_web_app/assets/140599598/d828cfc4-d17c-4c8f-8538-ca7a76340f27)
***
<p align="center"><b>🙌🏻 RUN RESULTS</b></p>
<p align="center"><a href="https://github.com/Katarzyna-SZ/REST_API_deployed_web_app/blob/main/REST%20API%20Demo.postman_test_run.json">Here is my collection file with the results. Enjoy!</a></p>

***

<a name='punkt6'>**📌 Summary**</a>

The repository contains documentation for an API testing project conducted using Postman. Throughout the project, tests were executed with thorough validation of request results. This validation process included checking the responses not only in the Postman environment but also cross-referencing them with the API documentation available in Swagger. Additionally, the results were verified on the GUI layer of the application, ensuring consistency and accuracy across different interfaces.

The documentation outlines the scope of work, which includes tasks such as creating test users, articles, and comments, as well as performing operations like updating and deleting them. It also provides examples of variables used in the testing process and explains the user authorization process.

Overall, the repository serves as a comprehensive guide to API testing using Postman, demonstrating the effective application of knowledge in real-world testing scenarios.

















