# Learning React.js
- Eve Porcello
- Started 11-06-2017

# Introduction
## Welcome
- We'll learn components and states
- Then dive into life cycles and states

## What you should know before watching this course
- This is an intro course but should have some knowledge of HTML and CSS
- You need to know some JavaScript
- We are using Node.js and npm
- Recommended Courses:
    - HTML5: Structure, Syntax, and Semantics with James Williamson
    - JavaScript Essential Training with Simon Allardice
    - Node.js Essential Training with Alex Banks

## Using the exercise files
- Each chapter has a folder
- The start folder is the blank file, end folder has the finished file
- Eve is using Sublime Text

# 1. What is React.js?
## What is React?
- User interface library
- Developed at Facebook
- Single page applications
- High-speed virtual DOM
- Functional programming is a programming paradigm
- Immutability
- Used in enterprise applications

## Why is React so fast?
- DOM rending speed
- Reading and writing to the dom is slow
- JS Objects are faster than DOM objects
- React Virtual DOM is a JS object
- Never reads from the real DOM
- Only writes to real DOM if needed

- When you use .getElementByID(), you are reading from the DOM
- When you are changing classes or content, you are writing to the DOM
- These processes slow down the application speed
- Other frameworks with BackboneJS also has this impediment

- React is fast because the JavaScript Logic deals only with the Virtual Dom
- The Virtual DOM then updates the DOM only with necessary updates

## Setting up React tools with Chrome
- Chome Web Store
- Get the "react-detector" by Kent Dodds, "React Developer Tools" by Facebook to Chrome
- Now when you visit a site like Airbnb, you can detect that it uses ReactJS
- The React Developer tools also adds a new tab to the panel (Ctrl + Shift + J)

# 2. Getting Started
## React.js syntax
- We can start by getting the scripts from React's website
- We add the scripts to the `<head>`
- We also add a `<script>` in our `<body>`
```js
<!DOCTYPE html>
<html>
    <head>
        <script src="https://fb.me/react-15.2.1.js"></script>
        <script src="https://fb.me/react-dom-15.2.1.js"></script>
        <title>My First React File</title>
    </head>
    <body>
        <div id='react-container'></div>
        <script>
            ReactDOM.render(
                React.createElement('div', null, 'Hello World'),
                document.getElementById('react-container'))
        </script>

    </body>
</html>
```

## Introducing JSX
- We are going to write React code but this can get messy
```js
ReactDOM.render(
    React.createElement('ul', null, 
        React.createElement('li', null, 'item 1'),
        React.createElement('li', null, 'item 2'),
        React.createElement('li', null, 'item 3')),
    document.getElementById('react-container'))
```
- So we use JSX  and tags instead
- We will get an error because browser does not recognize JSX
- Therefore we need Babel to transpile it
```js
ReactDOM.render(
    <ul>
        <li>item 1</li>
        <li>item 2</li>
        <li>item 3</li>
    </ul>
    document.getElementById('react-container')
)
```

## Preprocessing JSX with Babel
- Babel is
    - Transpile JavaScript Code
    - Works for JSX
    - Works for ES6 and beyond
- It will transpile new code (JSX) to old code that browsers can read
- The quickest way to add this is with a CDN and add it as another script tag
- This is not recommended for production since it is slower
- We'll learn about webpack bundling later
- We also need to add `type="text/babel"` to our script tag also

# 3. React Components
## What is a React component?
- Components are small user interface elements that changes over time
- Nordstrom uses a lot of React and uses lots of components
- You can browse it with React Developer Tools
- React can be used for an entire site or just small parts of it

## Creating a React component
- We are going to create a component
- It's best practice to capitalize a React component
```js
var MyComponent = React.createClass({
    render() {
        return <div>
            <h1>Hello World</h1>
            <p>This is my first React component!</p>
        </div>
    }
})

ReactDOM.render(
    <MyComponent />,
    document.getElementbyId('react-container')
)
```

## Creating React components with ES6
- We can use ES6 classes to create components
```js
class MyComponent extends React.Component {
    render() {
        return <div>
            <h1>Hello World</h1>
            <p>This is my first React component!</p>
        </div>
    }
}   

ReactDOM.render(
    <MyComponent />,
    document.getElementbyId('react-container')
)
```

## Creating React components as stateless components
- Stateless component is just a simple function that returns a React element
```js
const MyComponent = () => {
    return <div>
        <h1>Hello World</h1>
        <p>This is my first React component!</p>
    </div>
}
```