---
layout: single
title: "MERN Project 1 - How to setup project folder and push to git repository"
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

- Now in the 'server.js' file, we will listen for a port and set up out first route.

```javascript
const express = require('express')
const dotenv = require('dotenv').config()
const port = process.env.PORT || 5000

const app = express()

// our first route
app.get('/api/post',(req,res)) => {
  res.json({ message:'hello world'})
}


// listening
app.listen(port, () => console.log(`Server started on port ${port}`))
```

- Create the .env

```.env

NODE_ENV = development
PORT = 5000

```

- Next we can use a http client like postman to access our route. Just use the GET request 'http://localhost:5000/api/post'.

## Git repository

Run the following commands

- 'git init'
- 'git add .'
- 'git commit -m 'Initial commit'
