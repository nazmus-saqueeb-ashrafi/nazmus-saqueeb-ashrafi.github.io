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
# The App.js main component
function App() {
 
  return (
    
    <div className="App">
      
      <Box color={color}/>
      <Input onChange={onChange} color={color} />
      
    </div>
  );
}

export default App;
```



## useState hook

## Controlled input

## Prop drilling
