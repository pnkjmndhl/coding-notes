## React Notes

### JSX (JS + XML)
- stands for JavaScript for XML
- adds XML (and thus HTML) syntax in JS (and thus react)
- JSX tags have a tag name, attributes, and children (similar to XML)
- Similar to JS, quotes in JSX attributes represent strings. Numeric values and/or expressions should be wrapped in a curly brace.
- eg.
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

#### Since JSX is JS, identifiers such as `class` and `for` are discouraged as XML attribute names, as they have different meanings in JS
- use DOM property names like __className__ and __hmtlFor__ instead
    - DOM (Document Object Model), is a platform and language-neutral interface that allows programs and scripts to dynamically access and update the content, structure, and style of a document
- Basic React structure  :
```jsx
    let text = “lorem ipsum……”;
    reactDOM.render(
        <div>
            <a href=“#” className=“button”>Button</a>
        <div>{text}</div>
        </div>,
    document.getElementById(‘dom-node’)
    );
```
-  `reactDOM.render( )` function is used to declare the block of code that is used to render a React component into the DOM
-  `{text}` to render an expression you always need the curly braces
- `document.getElementById(‘dom-node’)` selects the DOM node that the component interacts with
- the block of code above should render as an anchor tag (or button) with some text right below it


#### hooks
- hooks are functions that let you "hook into" react state from function components. hooks let you use react without classes.
- react provides a few built in hooks
    - `useState`
        - eg. when you click the button, it increments value
            ```jsx
            import React, { useState } from 'react';
            function Example() {
            // Declare a new state variable, which we'll call "count"
            const [count, setCount] = useState(0);
            return (
                <div>
                <p>You clicked {count} times</p>
                <button onClick={() => setCount(count + 1)}>
                    Click Me
                </button>
                </div>
            );
            }
            ```
        - here `useState` is a hook, called inside a function component to add some local state to it. React preserves states during renders.