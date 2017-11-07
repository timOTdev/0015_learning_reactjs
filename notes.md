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

# 4. Props and States
## Using properties
- We are going to add some properties
- This makes it more dynamic and reusable
- Similar to adding attributes to HTML
- We use JSX expressions to print out the component
```js
class MyComponent extends React.Component {
    render() {
        return <div>
            <h1>{this.props.text}</h1>
            <p>{this.props.children}</p>
        </div>
    }
}   

ReactDOM.render(
    <div>
        <MyComponent text="Hello World">
            This is message 1
        </MyComponent>
        <MyComponent text="I am a Component">
            This is message 2
        </MyComponent>
        <MyComponent text="I have been reused!">
            This is message 3
        </MyComponent>
    </div>
    document.getElementbyId('react-container')
)
```

## Handling events
- We start with a single React file
- Later, we will build our app for production with webpack
- We add note sticky with buttons to edit and remove each sticky
```js
<!DOCTYPE html>
<html>
    <head>
        <script src="https://fb.me/react-15.2.1.js"></script>
        <script src="https://fb.me/react-dom-15.2.1.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.js"></script>
        <link rel="stylesheet" type="text/css" href="style.css">
        <title>Building the Note Board</title>
    </head>
    <body>
        <div id='react-container'></div>
        <script type="text/babel">
        var Note = React.createClass({
            edit() {
                alert("Editing Note")
            },

            remove() {
                alert("Removing Note")
            },

            render() {
                return (
                    <div className="note">
                        <p>{this.props.children}</p>
                        <span>
                            <button onClick={this.edit}>EDIT</button>
                            <button onClick={this.remove}>X</button>
                        </span>
                    </div>
                )
            }
        })

        ReactDOM.render(
            <Note>Hello World</Note>,
            document.getElementById('react-container')
        )
        </script>
    </body>
</html>
```

## Using state
- Here we are working with an example involved a checkbox
- It can either be checked or unchecked
```js
<!DOCTYPE html>
<html>
    <head>
        <script src="https://fb.me/react-15.2.1.js"></script>
        <script src="https://fb.me/react-dom-15.2.1.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.js"></script>
        <link rel="stylesheet" type="text/css" href="style.css">
        <title>Building the Note Board</title>
    </head>
    <body>
        <div id='react-container'></div>
        <script type="text/babel">
        var Checkbox = React.createClass({
            getInitialState() {
                return {checked: false}
            },
            handleCheck() {
                this.setState({checked: !this.state.checked})
            },
            render() {
                var msg
                if(this.state.checked) {
                    msg = "checked"
                } else {
                    msg = "unchecked"
                }
                return (
                    <div>
                        <input type="checkbox" 
                            onChange={this.handleCheck} />
                        <p>This box is {msg}</p>
                    </div>
                )
            }
        })

        ReactDOM.render(
            <Checkbox />
            document.getElementById('react-container')
        )
        </script>
    </body>
</html>
```

- If the initial box is checked
```js
<!DOCTYPE html>
<html>
    <head>
        <script src="https://fb.me/react-15.2.1.js"></script>
        <script src="https://fb.me/react-dom-15.2.1.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.js"></script>
        <link rel="stylesheet" type="text/css" href="style.css">
        <title>Building the Note Board</title>
    </head>
    <body>
        <div id='react-container'></div>
        <script type="text/babel">
        var Checkbox = React.createClass({
            getInitialState() {
                return {checked: true}
            },
            handleCheck() {
                this.setState({checked: !this.state.checked})
            },
            render() {
                var msg
                if(this.state.checked) {
                    msg = "checked"
                } else {
                    msg = "unchecked"
                }
                return (
                    <div>
                        <input type="checkbox" 
                            onChange={this.handleCheck}
                            defaultChecked={this.state.checked} />
                        <p>This box is {msg}</p>
                    </div>
                )
            }
        })

        ReactDOM.render(
            <Checkbox />
            document.getElementById('react-container')
        )
        </script>
    </body>
</html>
```

## Adding state to the note component
- Now back to our sticky note app
- We need to make a edit and delete function
- Eve also refactored to a ternary operator
```js
<!DOCTYPE html>
<html>
    <head>
        <script src="https://fb.me/react-15.2.1.js"></script>
        <script src="https://fb.me/react-dom-15.2.1.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.js"></script>
        <link rel="stylesheet" type="text/css" href="style.css">
        <title>Building the Note Board</title>
    </head>
    <body>
        <div id='react-container'></div>
        <script type="text/babel">
        var Note = React.createClass({
            getInitialState() {
                return {editing: false}
            },
            edit() {
                this.setState({editing: true})
            },
            save() {
                this.setState({editing: false})
            },
            remove() {
                alert("Removing Note")
            },
            renderForm() {
                return (
                    <div className="note">
                        <textarea></textarea>
                        <button onClick={this.save}>Save</button>
                    </div>
                )
            },
            renderDisplay() {
                return (
                    <div className="note">
                        <p>{this.props.children}</p>
                        <span>
                            <button onClick={this.edit}>EDIT</button>
                            <button onClick={this.remove}>X</button>
                        </span>
                    </div>
                )

            },
            render() {
                (this.state.editing) ? this.renderForm()
                                     : this.renderDisplay()
            }
        })

        ReactDOM.render(
            <Note>Hello World</Note>,
            document.getElementById('react-container')
        )
        </script>
    </body>
</html>
```

## Using refs
- `refs` are useful to access the underlying DOM node when we can't access via state or props
- So if we want to grab the value that the person types into the textarea
```js
       var Note = React.createClass({
            getInitialState() {
                return {editing: false}
            },
            edit() {
                this.setState({editing: true})
            },
            save() {
                var val = this.refs.newText.value
                alert('Later we will save this value: ' + val)
                this.setState({editing: false})
            },
            remove() {
                alert("Removing Note")
            },
            renderForm() {
                return (
                    <div className="note">
                        <textarea ref="newText"></textarea>
                        <button onClick={this.save}>Save</button>
                    </div>
                )
            },
            renderDisplay() {
                return (
                    <div className="note">
                        <p>{this.props.children}</p>
                        <span>
                            <button onClick={this.edit}>EDIT</button>
                            <button onClick={this.remove}>X</button>
                        </span>
                    </div>
                )

            },
            render() {
                (this.state.editing) ? this.renderForm()
                                     : this.renderDisplay()
            }
        })

        ReactDOM.render(
            <Note>Hello World</Note>,
            document.getElementById('react-container')
        )
```

## PropTypes
- We set up a `propTypes` to validate information coming in
- We don't want people to make more than 100 sticky notes or the app would break
- We set up a `propTypes` to help with this
- It is not required but a nice enhancement
- Here, we want the count to be number and to be less than 100
```js
       var Note = React.createClass({
            getInitialState() {
                return {editing: false}
            },
            edit() {
                this.setState({editing: true})
            },
            save() {
                var val = this.refs.newText.value
                alert('Later we will save this value: ' + val)
                this.setState({editing: false})
            },
            remove() {
                alert("Removing Note")
            },
            renderForm() {
                return (
                    <div className="note">
                        <textarea ref="newText"></textarea>
                        <button onClick={this.save}>Save</button>
                    </div>
                )
            },
            renderDisplay() {
                return (
                    <div className="note">
                        <p>{this.props.children}</p>
                        <span>
                            <button onClick={this.edit}>EDIT</button>
                            <button onClick={this.remove}>X</button>
                        </span>
                    </div>
                )

            },
            render() {
                (this.state.editing) ? this.renderForm()
                                     : this.renderDisplay()
            }
        })

        var Board = React.createClass({
            propTypes: {
                count: function(props, propName) {
                    if(typeof props[propName] !== "number") {
                        return new Error("The count must be a number")
                    }
                    if(props[propName] > 100) {
                        return new Error('Creating ' + props[propName] + ' notes is ridiculous')
                    }
                }
            },
            render() {
                return(
                    <div className='board'>
                        {this.props.count}
                    </div>
                )
            }
        })
        ReactDOM.render(
            <Board count={10}/>,
            document.getElementById('react-container')
        )
```

## Adding child elements
- We need to combine the Board and Note component
- The Board will be the parent that displays the notes that are held in state
- We need to change CSS also to make it work
    - Find the div.note 
    - Chane position to `relative`, instead of `absolute`
```js
       var Note = React.createClass({
            getInitialState() {
                return {editing: false}
            },
            edit() {
                this.setState({editing: true})
            },
            save() {
                var val = this.refs.newText.value
                alert('Later we will save this value: ' + val)
                this.setState({editing: false})
            },
            remove() {
                alert("Removing Note")
            },
            renderForm() {
                return (
                    <div className="note">
                        <textarea ref="newText"></textarea>
                        <button onClick={this.save}>Save</button>
                    </div>
                )
            },
            renderDisplay() {
                return (
                    <div className="note">
                        <p>{this.props.children}</p>
                        <span>
                            <button onClick={this.edit}>EDIT</button>
                            <button onClick={this.remove}>X</button>
                        </span>
                    </div>
                )

            },
            render() {
                (this.state.editing) ? this.renderForm()
                                     : this.renderDisplay()
            }
        })

        var Board = React.createClass({
            propTypes: {
                count: function(props, propName) {
                    if(typeof props[propName] !== "number") {
                        return new Error("The count must be a number")
                    }
                    if(props[propName] > 100) {
                        return new Error('Creating ' + props[propName] + ' notes is ridiculous')
                    }
                }
            },
            getInitialState() {
                return {
                    notes: [
                        'Call Bob',
                        'Email Sarah',
                        'Eat lunch',
                        'Finish proposal'
                    ]
                }
            }
            render() {
                return(
                    <div className='board'>
                        {this.state.notes.map((note, i) => {
                            return <Note key={i}>{note}</Note>
                        })}
                    </div>
                )
            }
        })
        ReactDOM.render(
            <Board count={10}/>,
            document.getElementById('react-container')
        )
```