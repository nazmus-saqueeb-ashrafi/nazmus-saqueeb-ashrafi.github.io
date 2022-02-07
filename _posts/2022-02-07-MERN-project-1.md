---
layout: single
title: "MERN Project 1 - How to setup project folder and push to git repository"
categories: MERN project
---

Hello. Welcome to this article which will be a guide for making a MERN stack application. In this first part we will learn how to setup an a project folder with some of the dependencies need to initialize the project. Just follow the steps.

## Setup

- Make a directory (with project name) and open VScode in it
- Make a folder called 'backend' in the root. Create file called 'server.js' in the backend folder. In 'server.js' console.log hello world if you want.
- Run 'npm init'
  - set 'server.js' as entry point
  - this will create a 'package.json' in the root
- Create a '.gitignore' file in the root and include 'node_modules' and '.env' in it.
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
  - this should output hello world for you.

And voila, you are all done setting up.

## Git repository

Run the following commands

- 'git init'
- 'git add .'
- 'git commit -m 'Initial commit'
