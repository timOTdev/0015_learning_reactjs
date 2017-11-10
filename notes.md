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
    - Change position to `relative`, instead of `absolute`
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

# 5. Enhancing Components
## Updating and removing notes
- Now we are making a update and remove notes component
```js
       var Note = React.createClass({
            getInitialState() {
                return {editing: false}
            },
            edit() {
                this.setState({editing: true})
            },
            save() {
                this.props.onChange(this.refs.newText.value, this.props.id)
                this.setState({editing: false})
            },
            remove() {
                this.props.onRemove(this.props.id)
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
                        {id: 0, note: 'Call Bob'},
                        {id: 1, note: 'Email Sarah'},
                        {id: 2, note: 'Eat Lunch'},
                        {id: 3, note: 'Finish proposal'},
                    ]
                }
            }
            update(newText, id) {
                var notes = this.state.notes.map(
                    note => (note.id !== id) ? 
                        note :
                        {
                            ...note,
                            note: newText
                        }
                    )
                this.setSate({notes})
            },
            remove(id) {
                var notes = this.state.notes.filter(note => note.id !== id)
                this.setState({notes})
            },
            eachNote(note) {
                return (<Note 
                            key={i}
                            id={note.id}
                            onChange={this.update}
                            onRemove={this.remove}>
                            {note.note}
                        </Note>)
            },
            render() {
                return(
                    <div className='board'>
                        {this.state.notes.map(this.eachNote)}
                    </div>
                )
            }
        })
        ReactDOM.render(
            <Board count={10}/>,
            document.getElementById('react-container')
        )
```

## Adding new notes
- We will now add a feature to add new notes
- We are not longer using the predefined notes
```js
       var Note = React.createClass({
            getInitialState() {
                return {editing: false}
            },
            edit() {
                this.setState({editing: true})
            },
            save() {
                this.props.onChange(this.refs.newText.value, this.props.id)
                this.setState({editing: false})
            },
            remove() {
                this.props.onRemove(this.props.id)
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
                    notes: []
                }
            },
            nextId() {
                this.uniqueId = this.uniqueId || 0
                return this.uniqueId++
            },
            add(text) {
                var notes = [
                    ...this.state.notes,
                    {
                        id: this.nextId(),
                        note: text
                    }
                ]
            },
            update(newText, id) {
                var notes = this.state.notes.map(
                    note => (note.id !== id) ? 
                        note :
                        {
                            ...note,
                            note: newText
                        }
                    )
                this.setSate({notes})
            },
            remove(id) {
                var notes = this.state.notes.filter(note => note.id !== id)
                this.setState({notes})
            },
            eachNote(note) {
                return (<Note 
                            key={i}
                            id={note.id}
                            onChange={this.update}
                            onRemove={this.remove}>
                            {note.note}
                        </Note>)
            },
            render() {
                return(
                    <div className='board'>
                        {this.state.notes.map(this.eachNote)}
                        <button onClick={() => this.add()}></button>
                    </div>
                )
            }
        })
        ReactDOM.render(
            <Board count={10}/>,
            document.getElementById('react-container')
        )
```

## Keys
- Keys help give children a unique ID so they render properly
- Children are usually passed among different components, so needs an idetifier
- This will also help maintain the state and properties correctly
- Here we are making the notes appear randomly on the board
- `componentWillMount()` fires before the render() method
- We also change the positioning in CSS to absolute
```js
       var Note = React.createClass({
            getInitialState() {
                return {editing: false}
            },
            componentWillMount() {
                this.style = {
                    right: this.randomBetween(0, window.innerWidth-150, 'px')
                    top: this.randomBetween(0, window.innerHeight-150, 'px')
                }
            },
            randomBetween(x, y, s) {
                return (x + Math.ceil(Math.random() *(y-x))) + s 
            },
            edit() {
                this.setState({editing: true})
            },
            save() {
                this.props.onChange(this.refs.newText.value, this.props.id)
                this.setState({editing: false})
            },
            remove() {
                this.props.onRemove(this.props.id)
            },
            renderForm() {
                return (
                    <div className="note"
                         style={this.style}>
                        <textarea ref="newText"></textarea>
                        <button onClick={this.save}>Save</button>
                    </div>
                )
            },
            renderDisplay() {
                return (
                    <div className="note"
                         style={this.style}>
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
                    notes: []
                }
            },
            nextId() {
                this.uniqueId = this.uniqueId || 0
                return this.uniqueId++
            },
            add(text) {
                var notes = [
                    ...this.state.notes,
                    {
                        id: this.nextId(),
                        note: text
                    }
                ]
            },
            update(newText, id) {
                var notes = this.state.notes.map(
                    note => (note.id !== id) ? 
                        note :
                        {
                            ...note,
                            note: newText
                        }
                    )
                this.setSate({notes})
            },
            remove(id) {
                var notes = this.state.notes.filter(note => note.id !== id)
                this.setState({notes})
            },
            eachNote(note) {
                return (<Note 
                            key={i}
                            id={note.id}
                            onChange={this.update}
                            onRemove={this.remove}>
                            {note.note}
                        </Note>)
            },
            render() {
                return(
                    <div className='board'>
                        {this.state.notes.map(this.eachNote)}
                        <button onClick={() => this.add()}></button>
                    </div>
                )
            }
        })
        ReactDOM.render(
            <Board count={10}/>,
            document.getElementById('react-container')
        )
```

## The component lifecycle
- Creates hooks for creation, lifetime, and teardown of components
- Allows you to add libraries, load data, etc. at specific times

### Mounting
- `getInitialState` allows you to set state of a component
- `componentWillMount` allows affecting state before render
- `render`
- `componentDidMount` fires after the render

### Updating
- `componentWillReceiveProps` allows to receive objects and affect state
- `shouldComponentUpdate` is for optimization, will only be called if something changes
- `componentWillUpdate` is for optimization, will only be called if something changes
- `render`
- `componentDidUpdate` fires after all DOM elements have been update

### Unmounting
- `componentWillUnmount` called before unmounting, all childrens of parents are also unmounted

## Mounting components
- We are going over `componentWillMount`, `componentDidMount`, `componentWillUnmount`
```js
<!DOCTYPE html>
<html>
    <head>
        <script src="https://fb.me/react-15.2.1.js"></script>
        <script src="https://fb.me/react-dom-15.2.1.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.js"></script>
        <style>
            #myDiv {
                background-color: blue;
                height: 200px;
                width: 200px;
            }
        </style>
        <title>Component Lifecycle</title>
    </head>
    <body>
        <div id='react-container'></div>
        <script type="text/babel">
            var Box = React.createClass({
                componentWillMount() {
                    alert('Component is about to mount')
                },
                componentDidMount() {
                    alert('Component just mounted')
                },
                render() {
                    return <div id='myDiv'></div>
                }
            })

            ReactDOM.render(
                <Box />,
                document.getElementById('react-container')
            )

            var getRidOfBox = document.getElementById('myDiv')
            getRidOfBox.onclick = function() {
                ReactDOM.unmountComponentAtNode(document.getElementById('react-container'))
                alert('Component is unmounted!')
            }
        </script>
    </body>
</html>
```

## Setting properties
- We are using component life cycles to set properties
- We are going to set some default props that are resusable
- We do this with `getDefaultProps()`
- I still don't understand how it's called with just `{this.props}`
- Notice we also have to change the style syntax
```js
<!DOCTYPE html>
<html>
    <head>
        <script src="https://fb.me/react-15.2.1.js"></script>
        <script src="https://fb.me/react-dom-15.2.1.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.js"></script>
        <title>Component Lifecycle</title>
    </head>
    <body>
        <div id='react-container'></div>
        <script type="text/babel">
            var Box = React.createClass({
                getDefaultProps() {
                    return {
                        backgroundColor: 'purple'
                        height: 200
                        width: 200
                    }
                }
                render() {
                    return <div id='myDiv'>
                        <div style={this.props}></div>
                        <section style={this.props}></section>
                    </div>
                }
            })

            ReactDOM.render(
                <Box />,
                document.getElementById('react-container')
            )
        </script>
    </body>
</html>
```

## Updating components
- Now we are going to the default styles in the state instead of `getDefaultProps()` component
- Upon clicking the note, it will turn red
- `componentDidUpdate()` also tells us that the update was complete
```js
<!DOCTYPE html>
<html>
    <head>
        <script src="https://fb.me/react-15.2.1.js"></script>
        <script src="https://fb.me/react-dom-15.2.1.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.js"></script>
        <title>Component Lifecycle</title>
    </head>
    <body>
        <div id='react-container'></div>
        <script type="text/babel">
            var Box = React.createClass({
                getInitialState() {
                    return {
                        backgroundColor: 'purple',
                        height: 200,
                        width: 200
                    }
                },
                update() {
                    this.setState({backgroundColor: 'red'})
                },
                componentDidUpdate() {
                    alert("Component did update")
                },
                render() {
                    return (<div style={this.state}
                                 onClick={this.update}>
                            </div>)
                }
            })

            ReactDOM.render(
                <Box />,
                document.getElementById('react-container')
            )
        </script>
    </body>
</html>
```

## Adding lifecycle methods to the bulletin board
- We now introduce Bacon API and React-Draggable API to the project
- We also made a method so that the old note is not deleted when we click edit
- We then added a draggable library so we can move the notes around
```js
<!DOCTYPE html>
<html>
    <head>
        <script src="https://fb.me/react-15.2.1.js"></script>
        <script src="https://fb.me/react-dom-15.2.1.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/1.0.0/fetch.js">
        </script>
        <script src="https://npmcdn.com/react-draggable"></script>
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
            componentWillMount() {
                this.style = {
                    right: this.randomBetween(0, window.innerWidth - 150, 'px'),
                    top: this.randomBetween(0, window.innerHeight -150, 'px')
                }
            },
            componentDidUpdate() {
                if (this.state.editing) {
                    this.refs.newText.focus()
                    this.refs.newText.select()
                }
            },
            shouldComponentUpdate(nextProps, nextState) {
                return this.props.children !== nextProps.children || this.state !== nextState
            },
            randomBetween(x, y, s) {
                return (x + Math.ceil(Math.random() * (y-x))) + s
            },
            edit() {
                this.setState({editing: true})
            },
            save() {
                this.props.onChange(this.refs.newText.value, this.props.id)
                this.setState({editing: false})
            },
            remove() {
                this.props.onRemove(this.props.id)
            },
            renderForm() {
                return (
                    <div className="note" 
                         style={this.style}>
                      <textarea ref="newText"
                                defaultValue={this.props.children}>
                      </textarea>
                      <button onClick={this.save}>SAVE</button>
                    </div>
                )
            },
            renderDisplay() {
                return ( 
                    <div className="note"
                         style={this.style}>
                        <p>{this.props.children}</p>
                        <span>
                          <button onClick={this.edit}>EDIT</button>
                          <button onClick={this.remove}>X</button>
                        </span>
                    </div>
                    )
            },
            render() {
              return ( <ReactDraggable>
                       {(this.state.editing) ? this.renderForm()
                                          : this.renderDisplay()}
                       </ReactDraggable>
                )

            }
        })

        var Board = React.createClass({
            propTypes: {
                count: function(props, propName) {
                    if(typeof props[propName] !== "number") {
                        return new Error("the count must be a number")
                    } 

                    if(props[propName] > 100) {
                        return new Error('Creating ' + props[propName] + ' notes is ridiculous')
                    }
                }
            },
            getInitialState() {
                return {
                    notes: []
                }
            },
            componentWillMount() {
                if (this.props.count) {
                    var url = `http://baconipsum.com/api/?type=all-meat&sentences=${this.props.count}`
                    fetch(url)
                          .then(results => results.json())
                          .then(array => array[0])
                          .then(text => text.split('. '))
                          .then(array => array.forEach(
                                sentence => this.add(sentence)))
                          .catch(function(err) {
                            console.log("Didn't connect to the API", err)
                          })
                }
            },
            nextId() {
                this.uniqueId = this.uniqueId || 0
                return this.uniqueId++
            },
            add(text) {
                var notes = [
                    ...this.state.notes,
                    {
                        id: this.nextId(),
                        note: text
                    }
                ]
                this.setState({notes})
            },
            update(newText, id) {
                var notes = this.state.notes.map(
                    note => (note.id !== id) ?
                       note : 
                        {
                            ...note, 
                            note: newText
                        }
                    )
                this.setState({notes})
            },
            remove(id) {
                var notes = this.state.notes.filter(note => note.id !== id)
                this.setState({notes})
            },
            eachNote(note) {
                return (<Note key={note.id}
                              id={note.id}
                              onChange={this.update}
                              onRemove={this.remove}>
                          {note.note}
                        </Note>)
            },
            render() {
                return (<div className='board'>
                           {this.state.notes.map(this.eachNote)}
                           <button onClick={() => this.add('New Note')}>+</button>
                        </div>)
            }
        })
        
        ReactDOM.render(<Board count={50}/>, 
            document.getElementById('react-container'))

        </script>
    </body>
</html>
```

# 6. Creating an App
## Using create-react-app
- Our local app is a single file and slows the load time
- We can download create-react-app to make the build process quicker
- It's a utility to set up react
- So you need Create-React-APP, NodeJS, and NPM installed globally
- We will install react globally and create a project:
1. `sudo npm install -g create-react-app`
2. Navigate to folder where you want to make the app in the terminal
3. `create-react-app <project name>`
4. Go into that directory and start the project by running `npm start`

## Launching the bulletin board app
1. Make sure you have a node_module folder
2. In src folder, App.js is the main file
    - We are going have it render our Board component
    - We rename App.js to Board.js
    - We also have Note.js for our Note component
3. We need to save React-draggable API as a dependency also
    - Use `npm install --save react-draggable`
4. Adjust index.js
    - Where our ReactDOM.render() is happening
5. Make sure our index.html has the correct div id of "react container"
6. Run the server with `npm start` to start our server
    - Use Ctrl + C to quit
7. Make a build production
    - Creates a build so our app is even more efficient

# Conclusion
## Next Steps
- Check out [React](https://reactjs.org/) to learn more
- Check out [React Native](https://facebook.github.io/react-native/) for mobile apps
- Check out [Flux](https://facebook.github.io/flux) for 
    - Use one way data flow paradigm
- Check out [Redux](https://redux.js.org/) for
    - Flux library that simplifies state in complicated applications