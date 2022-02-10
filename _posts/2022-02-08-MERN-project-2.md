---
layout: single
title: "MERN Project 2 - Controller, accept body data"
categories: MERN project
---

## Controller

We add the functionality of each routes a folder called 'controllers'. In the folder called 'controllers' we make a file called 'postController.js' which contains all the functionality related to posts. This keeps the functionality seperate from the routes, and therefore more our project is better organized.

```javascript
// backend/controllers/postController.js

// @desc    Get posts
// @route   GET /api/posts
// @access  Private
const getPosts = (req, res) => {
  res.status(200).json({ message: "get post" });
};

// @desc    Set posts
// @route   POST /api/posts
// @access  Private
const setPosts = (req, res) => {
  res.status(200).json({ message: "set post" });
};

module.exports = {
  getPosts,
  setPosts,
};
```

Changes are required in the 'postRoutes.js' file

```javascript
// backend/routes/postRoutes.js
const { getPosts, createPosts } = require("../controllers/postController");

router.get("/", getPosts);
router.post("/", setPosts);
```

If routes lead to the same path we can combine the routes to reduce code.

```javascript
// backend/routes/postRoutes.js
router.route("/").get(getPosts).post(setPost);
```

## Middleware to accept body data

To accept body data in the setPost function in the 'postRoutes.js' file we need to add some lines of middleware in our 'server.js' file.

```javascript
// backend/server.js
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
```
