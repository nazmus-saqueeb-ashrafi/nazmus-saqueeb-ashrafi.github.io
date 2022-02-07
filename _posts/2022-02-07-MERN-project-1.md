---
layout: single
title: "MERN Project 1 - How to setup project folder, push to git repository, setting up routes"
categories: MERN project
---

Hello. Welcome to this article which will be a guide for making a MERN stack application. In this first part we will learn how to setup an a project folder with some of the dependencies need to initialize the project. Just follow the steps.

## Setup

- Make a directory (with project name) and open VScode in it.
- Make a folder called 'backend' in the root. Create file called 'server.js' in the backend folder.
- Run 'npm init'
  - set 'server.js' as entry point
  - this will create a 'package.json' in the root
- Create a '.gitignore' file in the root and include

```.gitignore
node_modules
.env
```

- Run 'npm i express dotenv mongoose colors'
- Run 'npm i -D nodemon'
- Run these scripts in 'package.json'

```json
"scripts": {
    "start": "node backend/server.js",
    "server": "nodemon backend/server.js"
},
```

- Run 'npm run server'

And voila, you are all done setting up.

## Setting up routes

- Now in the 'server.js' file, we will listen for a port and set up a pointer to out routes.

```javascript
// server.js
const express = require("express");
const dotenv = require("dotenv").config();
const port = process.env.PORT || 5000;

const app = express();

// our route pointer
app.use("/api/posts", require(".routes/postRoutes"));

// listening
app.listen(port, () => console.log(`Server started on port ${port}`));
```

- Create the .env

```.env;

NODE_ENV = development;
PORT = 5000;
```

- create a folder named 'routes' and a file named 'postRoutes.js' in it.
  We keep our routes seperated from the 'server.js' file because we want to keep our routes in an organized fashion.

```javascript
//routes/postRoutes.js
const express = require("express");
const router = express.Router();

router.get("/", (req, res) => {
  res.status(200).json({ message: "get post" });
});

router.post("/", (req, res) => {
  res.status(200).json({ message: "set post" });
});

router.put("/:id", (req, res) => {
  res.status(200).json({ message: `update post ${req.params.id}` });
});

router.delete("/:id", (req, res) => {
  res.status(200).json({ message: `delete post ${req.params.id}` });
});
```

- Next we can use a http client like Postman to access our route. Just use the GET,POST,PUT,DELETE request 'http://localhost:5000/api/posts'.

## Git repository

Run the following commands

- 'git init'
- 'git add .'
- 'git commit -m 'Initial commit'
