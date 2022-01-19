---
layout: single
title: "React basics 1"
categories: technical
---

This article will discuss some of the core features of React. I have managed to get a grasp of few concepts within react by making a simple application (A color choser). This article will describe the concepts by explaining how the app was made.

There are four concepts which will be described in this article:

- React functional components
- useState hook
- Controlled input
- Prop drilling

## React functional components

Modern react uses functional components. In making this color chosser application, two components are used which are being imported to the App.js main component. These components are:

- The Box component
- The Input component


```javascript
// The App.js main component
function App() {
 
  return (
    
    <div className="App">
      
      <Box />
      <Input />
      
    </div>
  );
}

export default App;
```

```javascript
// The Input component
import React from 'react';

const Input = () => {
  return (
    <input
      autoFocus
      placeholder='Enter color here'
      
      
    />
  )
};

export default Input;
```

```javascript
// The Box component

const Box = () => {

  return (
    <div>
      <div style={{
          margin:'auto',
          width:'500px',
          height:'100px',
          border:'1px solid #000',
          textAlign: 'center',
          backgroundColor: color
      }}></div>

    </div>
    
  )
  
};

export default Box;
```



## useState hook

## Controlled input

## Prop drilling
