---
layout: single
title: "React basics 3 - React Router v6 routing, Context API, useParams, search functionality"
categories: technical
---

![Color Choser](/assets/images/routerandcontext.png)

Welcome to part 3 of my article on React basics. In this part we are going to learn about more concepts in React. Namely:

- React Router v6
- Context API
- useParams
- Implement search functionality

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

The context API is a built-in state management tool from React that can be used by us to manage all states and functions in a single file and declutter the App.js file. First we create a folder named context. In the context folder we create a file named DataContext.js.

```javascript
// The DataContext.js component
import { createContext, useState } from "react";

const DataContext = createContext({});

export const DataProvider = ({ children }) => {
  const [posts, setPosts] = useState([
    {
      id: 1,
      title: "My First Post",
      body: "Welcome to post 1 details",
    },
    {
      id: 2,
      title: "My 2nd Post",
      body: "Welcome to post 2 details",
    },
    {
      id: 3,
      title: "My 3rd Post",
      body: "Welcome to post 3 details",
    },
    {
      id: 4,
      title: "My Fourth Post",
      body: "Welcome to post 4 details",
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

## useParams

Now we are going to modify the app to make every blog title in the home page clickable. The click will lead to a page which shows the details of the blog. We will do this by importing useParams from react-router-dom and passing the id to through the url.

First we make out blog post titles into links which point to a custom route.

```javascript
// In Home.js component

<Link to={`/post/${post.id}`}>
  <h1>{post.title}</h1>
</Link>
```

Next we add the route in the App.js with leads to individual blog posts.

```javascript
// In App.js component

<Route path="/post/:id" element={<PostPage />} />
```

Last step is to actually create the PostPage component. Note that this component uses useParam to get the post id from the url. The id is the compared and the matching post's body is then viewed in the page.

```javascript
// The PostPage.js component

import React from "react";
import { useParams } from "react-router-dom";

import { useContext } from "react";
import DataContext from "./context/DataContext";

const PostPage = () => {
  const { posts } = useContext(DataContext);

  const { id } = useParams();
  const post = posts.find((post) => post.id.toString() === id);

  return <div>{post.body}</div>;
};

export default PostPage;
```

## Implement search functionality

In this part we are going to modify our app to inclue search functionality. As we are using the context API as the one true source of data in our app, our first step will be to include states required by the search functionality in our DataContext.js file.

```javascript
// DataContext.js
const [search, setSearch] = useState("");
const [searchResults, setSearchResults] = useState([]);
```

Next we will create an input in our Nav component. The input will be a [controlled input](https://nazmusashrafi.github.io/technical/react-basics-1/#controlled-input-and-prop-drilling) which will will be changing our search state. The Nav component will get the search and setSearch state from the DataContext.

```javascript
// Nav.js

const {search,setSearch} = useContext(DataContext)

<input
  type="text"
  value={search}
  onChange={(e)=>{
    setSearch(e.target.value)
  }}
/>

```

Next up, we write a useEffect which filters our result depending on what we searched for each time the search or posts state changes. We also set the searchResult state to our filtered results.

```javascript
// DataContext.js

useEffect(() => {
  const filteredResults = posts.filter(
    (post) =>
      post.body.toLowerCase().includes(search.toLowerCase()) ||
      post.title.toLowerCase().includes(search.toLowerCase())
  );

  setSearchResults(filteredResults.reverse());
  // we use revese to show the newest posts first
}, [posts, search]);
```

Lastly we change what the Home.js file maps because we want this mapping to change based on our search. We no longer use posts to map, now we use searchResults to map.

```javascript
// Home.js
const { searchResults } = useContext(DataContext);

return (
  <div>
    {searchResults.map((post) => {
      return (
        <div>
          <Link to={`/post/${post.id}`}>
            <h1>{post.title}</h1>
          </Link>
          <p>{post.datetime}</p>
        </div>
      );
    })}
  </div>
);
```
