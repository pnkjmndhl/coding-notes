## React Notes
- react is a tool for building UI components, sometimes referred to as front JavaScript framework
- instead of manipulating the browser's DOM directly, react creates a virtual DOM in memory, where it does all the necessary manipulating, before making changes to the brower DOM
    - DOM (Document Object Model) that defines logical structure of documents (HTML or XML) and the way a document is accessed and manipulated
    - DOM represents the page as nodes and objects (eg. title, body, url), such that programming languages can interact with it easily
    - eg. 
    ```js
    console.log(document.title)
    var newEle = document.createElement("h3");
    newEle.textContent = "new text";
    document.querySelector("body").appendChild(newEle);
    ```
- browser DOM vs virtual DOM
    - <img src="https://static.javatpoint.com/tutorial/reactjs/images/what-is-dom-in-react3.jpg" width="500" height="300"/>
    - faster since all the page is not loaded at once
    - eg. facebook, first the information is in the virtual dom, and later loads on browser
- react only makes the required changes


### react uses ES6
- see [ES6](es6.md) notes
### react render HTML
- react renders HTML to a web page, using `ReactDOM.render([html-code],[html-element])`


### react JSX (JS + XML)
- allows XML (and thus HTML) in JS (and thus react)
- JSX tags have a tag name, attributes, and children (similar to XML)
- Similar to JS, quotes in JSX attributes represent strings. Numeric values and/or expressions should be wrapped in a curly brace.
- makes it easier to write react applications
- eg.
```jsx
//using JSX
const myElement = <h1>I Love JSX!</h1>;
//without JSX
const myElement = React.createElement('h1', {}, 'I do not use JSX!');

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement);
```
- JSX is translated to JS at runtime
- `class` is used in HTML, but since JSX in rendered in JS, class keyword is reserved for JS, so instead `className` is used
- when JSX is rendered to JS, `className` is converted to `class`

eg.
```xml
<div className =“red”>Children Text</div>;
<myCounter count={3 + 5} />;
var gameScores = {
    player1  :   2,
    player2  :   5
};
<DashboardUnit data-index=“2”>
    <h1>Scores</h1>
    <Scoreboard className=“results” scores={gameScores} />
</DashboardUnit>;
```
- `<myCounter>` has an attribute called count that takes a numeric expression as its value
- `gameScores` is an object literal that has two prop-value pairs
- `<DashboardUnit>` is the block of XML that gets rendered on the page
- `scores={gameScores}` : the scores attribute gets a value from the gameScores object that was defined earlier

### react components
- independent and reusable bits of code, same as JS functions but work in isolation and returns HTML
- types: class components and function components
    - class component:
        - includes `extends React.Component` statement, that creates an inheritance to React.Component, and gives your component access to React.Component's functions
        - includes `render()` method that returns HTML
    - function component:
        - less code, easier to understand
- rendering a component:
    ```jsx
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<Car />);
    ```
- props (stands for properties)
    - react components use prop to communicate with each other
    - like HTML attributes, but you can also pass objects, arrays and functions through them
    - like function arguments, and you send them into the component as attributes
- components can exist inside other components
- components can independently exist in separate files

### react classes
- before react 16.8, only classes could track state and lifecycle of react component
- with the addition of hooks, function components are now equivalent to class components
- [read more](https://www.w3schools.com/react/react_class.asp)

### react events
- same events as HTML, but camelCase, `onclick`->`onClick`
- handlers in curly braces, `onClick="shoot()"`->`onClick={shoot}`


### react router
- `npm i -D react-router-dom`


### hooks and states
- hooks are functions that let you "hook into" react state from function components. hooks let you use react without classes.
- react provides a few built in hooks
- state of a component is the data being used in that component (that point in time)
- could be array of values: `96`, strings: `"apple"`, boolean: `0`, objects, or any data used by component
- if you want to change a **reactive variable** over time, with some events (such as user clicking ..)
    - a reactive variable (hook, eg. `useState`) watches the change in value
    - eg. when you click the button, it increments value
        ```jsx
        import React, { useState } from 'react';
        function Example() {
        // Declare a new state variable, which we'll call "count"
        const [count, setCount] = useState(0); //count = 0, and setCount updates count
        //
        const handleClick = () => {
            setCount(count + 1)
        }
        
        return (
            <div>
            <p>You clicked {count} times</p>
            <button onClick={handleClick}>
                Click Me
            </button>
            </div>
        );
        }
        ```


### redux (state management library)
  - predicatable state container for JavaScript apps (React, Angular, Vue or vanilla JS)
    - stores state of an application
  
