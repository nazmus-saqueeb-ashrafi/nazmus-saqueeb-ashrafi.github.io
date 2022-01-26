---
layout: single
title: "React basics 2"
categories: technical
---

![Api Fetch](/assets/images/apifetch.png)

This is the second part of React basics. In this article we will learn about:

- useEffect hook
- Fetching data from an API

We will learn about the concepts above by creating a simple app that fetches data from a fake API for testing. This API has different material at different endpoints. We will attempt to populate our app with data from 3 different endpoints based on the button the user has clicked.

## useEffect hook and fetching data from an API

We use a useEffect hook to execute functionality whenever a state is changed. By default the hook is set to execute functionality when the page loads, but we can change that based on what event we want to happen for the functionality to execute.

```javascript
// This content is in App.js

import { useEffect, useState } from "react";

const [reqType, setReqType] = useState("users");
const [data, setData] = useState([]);

useEffect(() => {
  const fetchData = async () => {
    const response = await fetch(
      `https://jsonplaceholder.typicode.com/${reqType}`
    );
    const data = await response.json();

    setData(data);
  };

  fetchData();
}, [reqType]);
```

Shown above is a useState called reqType which we will use use to describe the type of request made by the user. Also shown is a useEffect hook which is set to execute every time our reqType state is changed. Also notice that we are using our reqType to change the url and fetch the related content from the API.

Inside the useEffect hook we have made and called a function called fetchData which can be used to fetch data from the mock API every time the reqType is changed. The data is then set in our data useState. This data is then mapped and displayed in our app using a table.

```javascript
// This content is in App.js

return (
  <div className="App">
    <table>
      <tbody>
        {data.map((entry) => {
          return (
            <tr>
              {Object.entries(entry).map(([key, value]) => {
                return <td key={key}>{JSON.stringify(value)}</td>;
              })}
            </tr>
          );
        })}
      </tbody>
    </table>
  </div>
);
```

All thats left now to do is to create a way our user can change the reqType useState. To do this we will create a React component called customButton and pass the setReqType as a prop. We also pass a name from the button as a prop which will be used to both name the button and also to set the reqType and thus changing the url we fetch from in the useEffect and hence the data displayed in out app.

```javascript
// This content is in CustomButton.js

import React from "react";

const CustomButton = ({ name, setReqType }) => {
  const handleOnClick = () => {
    setReqType(name);
  };

  return <button onClick={handleOnClick}>{name}</button>;
};

export default CustomButton;
```

```javascript
// This content is in App.js

<div className="App">
  <CustomButton name="users" setReqType={setReqType} />

  <CustomButton name="posts" setReqType={setReqType} />

  <CustomButton name="comments" setReqType={setReqType} />

  <table></table>
</div>
```
