---
layout: single
title: "React basics 1"
categories: technical
---

This article will discuss some of the core features of React. I have managed to get a grasp of few concepts within React by making a simple application (A color choser). This article will describe the concepts by explaining how the app was made.

There are four concepts which will be described in this article:

- React functional components
- useState hook
- Controlled input
- Prop drilling

## React functional components

Modern react uses functional components. In making this color choser application, two components are used which are being imported to the App.js main component. These components are:

- The Box component
- The Input component


```javascript
// The App.js main component

import Box from './Box';
import Input from './Input';

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
      <div style={
          margin:'auto',
          width:'500px',
          height:'100px',
          border:'1px solid #000',
          textAlign: 'center',
          backgroundColor: green
      }></div>

    </div>
    
  )
  
};

export default Box;
```

Notice that the default color of the Box component is set to green. We will use a useState hook to avoid hardcoding the background color in the next section.



## useState hook

We will use the useState hook to set an initial color of empty. The idea is to take input from the user to set the color. The user input will then be used to change the color of the box in the next section.

```javascript

import Box from './Box';
import Input from './Input';

import React, { useState } from 'react';

function App() {

  const [color,setColor] = useState('')

  
  return (
    
    <div className="App">
      
      <Box/>
      <Input/>
      
    </div>
  );
}

export default App;
```


## Prop drilling and controlled input

The useState hook and onChange function will be written in the main App.js component which acts as the parent component in our app. We will drill these properties down to our children components. This way the Box and Input components can use the useState hook and onChange function.

Also notice what our onChange function does. It takes takes the value from the event and uses the hook to change the value of the color. We will also set the value of the event using the user input. The value of the input is also set to color which is the hook. This will make our input a controlled input.

```javascript

import Box from './Box';
import Input from './Input';

import React, { useState } from 'react';


function App() {

  const [color,setColor] = useState('')


  const onChange = (e) => {
      
    setColor(e.target.value)
    
  }

  
  return (
    
    <div className="App">
      
      <Box color={color}/>
      <Input onChange={onChange} color={color} />
      
    </div>
  );
}

export default App;

```


```javascript

const Input = ({onChange, color}) => {
  return (
    <input
      autoFocus
      onChange={onChange}
      placeholder='Enter color here'
      value={color}
      
    />
  )
};

export default Input;

```

```javascript

const Box = ({color}) => {

    
  return (
    <div>
      <div style={
          margin:'auto',
          width:'500px',
          height:'100px',
          border:'1px solid #000',
          textAlign: 'center',
          backgroundColor: color
      }>{color?color:"This is empty"}</div>

    </div>
    
  )
  
};

export default Box;


```










