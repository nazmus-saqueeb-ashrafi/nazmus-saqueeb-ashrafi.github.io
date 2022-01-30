---
layout: single
title: "React basics 3 - React Router v6 and Context API"
categories: technical
---

![Color Choser](/assets/images/routerandcontext.png)

Welcome to part 3 of my article on React basics. In this part we are going to learn about 2 very important concepts in React. Namely:

- React Router v6
- The Context API

As usual I will attempt to explain things with the help of a simple app. This app consists of a navigation bar with 3 links which always stays on the page. The links utilizes React Router and so the switch between the links is lightning fast. We are also going to use the context API to generate the posts when the home link is clicked. The footer component is also always present on the page.

## React Router v6 routing

We set up the Router which contains Routes which contain Route. Route is the component which takes in other components and the path to those components as parameters.

```javascript
// The App.js main component

import "./App.css";
import Nav from "./Nav";
import Home from "./Home";
import Blog from "./Blog";
import About from "./About";
import Footer from "./Footer";

import { BrowserRouter as Router, Route, Routes } from "react-router-dom";

function App() {
  return (
    <div className="App">
      <Router>
        <Nav />
        <Routes>
          <Route path="/" element={<Home />} />

          <Route path="/blog" element={<Blog />} />

          <Route path="/about" element={<About />} />
        </Routes>
        <Footer />
      </Router>
    </div>
  );
}

export default App;
```

In the Nav component the links has to be surrounded by Link component from the React Router module so that the paths can be accessed. This will complete our routing and all the link will work.

```javascript
// The Nav.js component

import React from "react";
import { Link } from "react-router-dom";

const Nav = () => {
  return (
    <nav style={{ backgroundColor: "silver" }}>
      <ul>
        <li>
          <Link to="/">Home</Link>
        </li>
        <li>
          <Link to="/blog">Blog</Link>
        </li>
        <li>
          <Link to="/about">About</Link>
        </li>
      </ul>
    </nav>
  );
};

export default Nav;
```

## Context API

The context API is a built in state management tool from React that can be used by us to manage all states and functions in a single file and declutter the App.js file. First we create a folder named context. In the context folder we create a file named DataContext.js.

```javascript
// The DataContext.js component
import { createContext, useState } from "react";

const DataContext = createContext({});

export const DataProvider = ({ children }) => {
  const [posts, setPosts] = useState([
    {
      id: 1,
      title: "My First Post",
    },
    {
      id: 2,
      title: "My 2nd Post",
    },
    {
      id: 3,
      title: "My 3rd Post",
    },
    {
      id: 4,
      title: "My Fourth Post",
    },
  ]);

  return (
    <DataContext.Provider
      value={{
        posts,
        setPosts,
      }}
    >
      {children}
    </DataContext.Provider>
  );
};

export default DataContext;
```

Next we wrap our components in the DataProvider we exported from the DataContext.js file. This will allow any components wrapped in the DataProvider to receive data from the DataProvider.

```javascript
// The App.js main component

import "./App.css";
import Nav from "./Nav";
import Home from "./Home";
import Blog from "./Blog";
import About from "./About";
import Footer from "./Footer";
import { DataProvider } from "./context/DataContext";

import { BrowserRouter as Router, Route, Routes } from "react-router-dom";

function App() {
  return (
    <div className="App">
      <Router>
        <DataProvider>
          <Nav />
          <Routes>
            <Route path="/" element={<Home />} />

            <Route path="/blog" element={<Blog />} />

            <Route path="/about" element={<About />} />
          </Routes>
          <Footer />
        </DataProvider>
      </Router>
    </div>
  );
}

export default App;
```

The Home component receives the posts from the DataProvider using the useContext hook provided by the Context API. The posts are then mapped and viewed in our app.

```javascript
// The Home.js component

import { useContext } from "react";
import DataContext from "./context/DataContext";

const Home = () => {
  const { posts } = useContext(DataContext);

  return (
    <div>
      {posts.map((post) => {
        return <h1>{post.title}</h1>;
      })}
    </div>
  );
};

export default Home;
```
