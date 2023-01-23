

#### HTML tags vs. React Components  :
-  To render an HTML tag use lower-case tag names (like usual)  eg.
```jsx
const myDiv  =  <div className=“foo” />;
ReactDOM.render( myDiv, document.getElementById(‘dom-node’) );
```          
- a `<div>` is stored in a `const` called `myDiv` and then rendered using the `ReactDOM.render()` function
- The function takes two args, the `<div>` stored in myDiv and `document.getElementById()` method which is used to select the node in the DOM tree that React interacts with               

- To render a React Component you need to declare a local variable in [Pascal case](http://c2.com/cgi/wiki?PascalCase) E.g
```jsx
const MyComponent  =  React.createClass( {/*….*/} );
const myElement        =  <MyComponent someProperty={true} />;
ReactDOM.render( myElement, document.getElementById(‘dom-node’) ) ;
```
- The `React.createClass()` function is initiated as a value for `MyComponent` & this enables `MyComponent` to be recognized as a React component class.
- After the React component has been created it is then passed as a value to a `const` called myElement. A property has also been defined and the value has been set to a boolean (`someProperty={true}`)
- The `ReactDOM.render()` function then takes two args; the React component that was stored in `myElement` and `document.getElementById()` method which selects the specific DOM node that React interacts with

## Virtual DOM
- React uses the [virtual DOM](http://tonyfreed.com/blog/what_is_virtual_dom) to clone a node that already exists in the DOM
- Subtrees are created in the virtual DOM and then rendered based on state changes
- When a state change occurs two things happen:
    - React runs a diff to check what changed
    - Then it updates the DOM based on the result of that diff (Referred to as [reconciliation](https://facebook.github.io/react/docs/reconciliation.html))
- The Virtual DOM is considered the magic behind React. It batches DOM operations to keep everything quick and snappy because DOM manipulation is SLOW 
- Once a state is changed it triggers the [diff algorithm](https://facebook.github.io/react/docs/reconciliation.html) to check all components, re-rendering only those that have changed properties. 

## Boilerplate Notes

- When naming the Component.jsx file always make sure to use [PascalCase]((http://c2.com/cgi/wiki?PascalCase)  E.g : Hello.jsx, World.jsx or HelloWorld.jsx

- Don’t render code within the Component.jsx file. For instance this should be avoided:
```jsx
// Hello.jsx
import React from 'react';
import ReactDOM from 'react-dom';

class Hello extends React.Component{
    render(){
        return <h1>Hello</h1>
    }
}

ReactDOM.render(<Hello/>, document.querySelector('#hello'));
```
- The block above should be avoided because the Component.jsx file must be a module and it must export the code that is meant to be public. E.g
```jsx
// Hello.jsx
import React from 'react';

class Hello extends React.Component{
    render(){
      return <h1>Hello</h1>
    }
}

export default Hello;
```
- By doing this you allow the modular component to be included via `import` e.g
```js
// index.js
import Hello from ‘./Components/Hello/Hello.jsx’; // <Hello />

import WhateverDefaultExists from ‘./Components/Hello/Hello.jsx’ // <WhateverDefaultExists />
```

- In [ES6](https://goo.gl/7EYqev) there are two kinds of exports: [named exports (several per module) and default exports (one per module)](http://www.2ality.com/2014/09/es6-modules-final.html)

- Use named exports when your module needs to export multiple variables/functions, and use a default export when your module only needs to export one variable/function

- In a nutshell, `./webpack.config.js` will define the entry file(s) (index.js), and the entry file executes code while all other files simply export modules

- __This applies to ALL JS modules not just React Components__ 

### [CSS Modules](https://github.com/gajus/react-css-modules#css-modules)

- Each component has a Component.css file that contains local scoped styles (specific to that component). E.g
```markdown
-Components
    -Hello
      -Hello.css
      -Hello.jsx
```
- To scope the styles to the Hello component we need to structure Hello.jsx similar to :  
```javascript
import React from 'react';
import CSSModules from 'react-css-modules';
import styles from './Hello.css';

class Hello extends React.Component {
    render() {
      return <h1 className='test' styleName='test'>Hello {this.props.name}</h1>;
    }
}

export default CSSModules(Hello, styles);
```
- The `CSSModules` component is imported to enable the use of `styleName` prop. In the block above the difference between `className` and `styleName` is that the former is meant to be a global CSS class while the latter is meant to be CSS Modules class (locally scoped to the Hello component).

- By adopting this approach there is a clear distinction between global CSS and CSS Modules. The output looks similar to : 
```html
  <h1 class="test Components-World-___World__test___1lmut">Hello</h1> 
```
## Working with Props 

- Each component has a set of `propTypes` that define certain attributes/properties associated with that given component
 
- `propType` is a static method declared within a React.Component, it defines the properties and their type/requirement
 
- `React.PropTypes` is the object that defines the validators
 
```javascript
// Component.jsx
static propTypes = {
   myProp: PropTypes.string,
   myRequiredProp: PropTypes.string.isRequired
};
```
- You won't use `propTypes` or `React.Proptypes` for any other reason see : [https://facebook.github.io/react/docs/reusable-components.html](https://facebook.github.io/react/docs/reusable-components.html)

- `propTypes` can be declared within the Component.jsx file or in the entry file where the component is being rendered 

- Defined properties can be accessed via `this.props` e.g
```javascript
//Component.js
class Hello extends React.Component {
    render() {
      return <h1 className='test' styleName='test'>Hello {this.props.name}</h1>;
    }
}

//entry.js
ReactDOM.render(<Hello name="Test" />, hello);
```
- The `PropTypes` method is part of the React object and so it becomes available once React has been imported into a component 

- It is considered best practice to define properties specific to a component with the respectful [React.PropTypes validator](https://facebook.github.io/react/docs/reusable-components.html#prop-validation) as this helps with debugging especially when an expected prop is missing or has the wrong type

- A common way to use `propTypes` is similar to : 
```javascript 
//Component.jsx
class Component extends React.Component{
  static propTypes = {
    name: React.PropTypes.isRequired
  }; 
  static defaultProps = {
    name: 'world'
  };
  render() {
    return <div>hello {this.props.name}</div>
  }
}
```
- What this does is to tell React that `name` is a `PropType` that needs to have a value in order to render the component (`isRequired`). 

- If there is no value passed it will return an error in your console

- To prevent syntax repetition when using `PropTypes` you can [destructure](https://github.com/DrkSephy/es6-cheatsheet#destructuring) the `PropTypes` method from the `React` object in order to use it without reference     

- This can be done when you `import` React into the Component.jsx file E.g

``` import React, { PropTypes } from 'react'; ``` 

- Now `PropTypes` can be accessed without referencing the `React` object E.g
```jsx
static propTypes = {
  title: PropTypes.isRequired
};
```
- As opposed to :  
```jsx
static propTypes = {
  title: React.PropTypes.isRequired
};        
```
- As mentioned earlier, you can use the `this` keyword to access properties of a component. Using the `title` example above the code may look like this :  
```jsx
  <h3 styleName='title'>{this.props.title}</h3> 
```
- To prevent `this` syntax repetition we can use [destructuring](https://github.com/DrkSephy/es6-cheatsheet#destructuring) again to extract `this.props` from the expression E.g
```jsx
...
render(){
  const { title, children, isOpen } = this.props;
  return <h3 styleName='title'>{title}</h3>;
}   
```
- What happened is that we have declared some constants (`const`) associated with our component and these constants also happen to be props that we defined earlier. So we can extract the `props` from the expression `this.props` so that they can be used without reference. They are still associated with the component. 

## More on Destructuring
```javascript
class FancyDiv extends React.Component {
  render() {

    const { foo, ...otherProps } = { foo: 'foo', bar: 'bar', 'xyz': 111 };
    foo; // returns 'foo'
    otherProps; // { bar: 'bar', 'xyz': 111 }
    otherProps.foo // undefined
    otherPops.bar; // 'bar'
    otherPops.xyz; // 111
    
    const foo = 'foo';
    const bar = 'bar';
    const myObject = { foo, notBar: bar };     // { foo: 'foo', notBar: 'bar' }


    const { className, children, ...props } = this.props;
    const actualClassName = 'goodbye ' + className;
    return <div className={actualClassName} {...props}>{children}</div>;
  }
}

ReactDOM.render(<FancyDiv className="hello">Hello!</FancyDiv>, dom-node); 
```
#### To further understand destructuring I'm going to explain what is going on in the code above :  

- We have defined a constant (`const`) and assigned an object as its value

- Inside that `const` there is a variable that looks like this : `...otherProps`. It is called a [spread operator](https://facebook.github.io/react/docs/jsx-spread.html)

- The spread operator is used to extract values from the object that was assigned, and since `foo` has been destructured it is not extracted into the spread operator. 

- So `otherProps.foo` returns `undefined`

- While `otherProps` returns `{ bar: 'bar', 'xyz': 111 }`

- You can access a key in the object using `otherProps` like so :  

```js
 otherProps.bar; //returns 'bar'
 otherProps.xyz; //returns 111 
```
- Let's see how this may be used with a component: 

```javascript
const { className, children, ...props } = this.props;
const actualClassName = 'goodbye ' + className;
return <div className={actualClassName} {...props}>{children}</div>;

ReactDOM.render(<FancyDiv className="hello">Hello!</FancyDiv>, accordion);
```
- In the code above we destructure `className`, `children`, `...props` from the expression (`this.props`) 

- We then define a new constant (`const`) and assign it a string (`goodbye`) and a variable that was extracted earlier (`className`)

- When the next line runs, the `<div>` is rendered to the page, we assign that new constant as the `className` and then pass along the variable `...props` as an attribute to the same `<div>`

- Since there is already a `className` variable that was destructured in our original set of constants we have access to it through `this.props`.

- So the code that gets run will look similar to : `this.props.className`, thereby referencing another className on the `<div>` and this makes it possible to have those two class names associated with the same `<div>` E.g
```
        <div class="goodbye hello">
```
- The `hello` is passed as a value to the 'className' attribute when the `<div>` is rendered     

## Adding component props 
Let's update the example above to accept properties.

- Import `React.PropTypes` for [prop validation][0]
- Add `static propTypes` to define available props
- Add `static defaultProps` to define default values

### MyComponent.js
```js
import React, { Component, PropTypes } from 'react';

class MyComponent extends Component {
    static propTypes = {
        name: PropTypes.string.isRequired
    };
    static defaultProps = {
        name: 'World'
    };
    render() {
        return <div>Hello {this.props.name}!</div>;
    }
}

export default MyComponent;
```

### example.js
```js
import React from 'react';
import ReactDOM from 'react-dom';
import MyComponent from './MyComponent.js';
const el = document.getElementById('example');

// <div>Hello World!</div>
ReactDOM.render(<MyComponent />, el);

// <div>Hello Friend!</div>
ReactDOM.render(<MyComponent name="Friend" />, el);
```
## Passing down standard attributes along with props
A common pattern when building React components is to extend a native DOM element, allowing any standard attribute to be passed down. 

In the example above, we may want to set `className` or `style`, however these attributes will be ignored as `render` does not pass these properties to the `<div>` being returned.

The code can be re-written to use [object destruction][0] to extract our custom defined props and pass through all other properties.

```js
class MyComponent extends Component {
    render() {
        const { name, ...props} = this.props;
        return <div {...props}>Hello {name}!</div>;
    }
}
```

Now any extra props will be passed down to the `<div>` being rendered...

```js
// <div class="myClass">Hello World!</div>
ReactDOM.render(<MyComponent className="myClass" />, el);

// <div style="background: lime;">Hello World!</div>
ReactDOM.render(<MyComponent style={{ background: 'lime' }} />, el);
```
## Working with children

The DOM is a nested tree of elements. Separate your UI into multiple components to handle their own rendering. 


### ListComponent.js

```js
class ListComponent extends Component {
    static propTypes = {
        children: PropTypes.node.isRequired
    };
    render() {
        const { children } = this.props;
        return <ul>{children}</ul>;
    }
}

export default ListComponent;
```

### ItemComponent.js
```js
class ItemComponent extends Component {
    static propTypes = {
        name: PropTypes.string.isRequired
    };
    render() {
        const { name } = this.props;
        return <li>{name}</li>;
    }
}

export default ItemComponent ;
```

### example.js
```js
// <ul>
//     <li>Item #1</li>
//     <li>Item #2</li>
//     <li>Item #3</li>
// </ul>
ReactDOM.render(<ListComponent>
    <ItemComponent name="Item #1" />
    <ItemComponent name="Item #2" />
    <ItemComponent name="Item #3" />
<ListComponent>, el);
```
## [Dynamic children][0]
When creating dynamic children, the `key` prop must be specified to uniquely identify each child node. For example, the above `ListComponent` can written without the need for `ItemComponent`.

### ListComponent.js

```js
class ListComponent extends Component {
    static propTypes = {
        items: PropTypes.array.isRequired
    };
    render() {
        const { items } = this.props;
        return <ul>{items.map((item, i) => {
            return <li key={i}>{item}</li>;
        })}</ul>;
    }
}
```

### example.js
```js
const items = ['Item #1', 'Item #2', 'Item #3'];
ReactDOM.render(<ListComponent items={items} />, el);
```
## Event handling
Here is an example of a component that requires a callback property `onButtonClick` to handle the `onClick` event. Key notes:

- `onButtonClick` property added to `propTypes` and default handler added to `defaultProps`
- `handleClick` method is used as a wrapper (we could have just passed `onClick` prop directly)
- [`constructor` must bind `this` to the `handleClick` event handler method for ES6 classes][0]
- `render` extracts `onButtonClick` from props to prevent passing down to `<button>`

### ButtonComponent.js

```js
class ButtonComponent extends Component {
    static propTypes = {
        text: PropTypes.string.isRequired,
        onButtonClick: PropTypes.func.isRequired
    };
    static defaultProps = {
        type: 'button',
        text: 'Click Me!',
        onButtonClick() {
            alert('Button Clicked!');
        }
    };
    constructor(props) {
        super(props);
        this.handleClick = this.handleClick.bind(this);
    }
    handleClick(e) {
        e.preventDefault();
        this.props.onButtonClick();
    }
    render() {
        const { text, onButtonClick, ...props } = this.props;
        return <button onClick={this.handleClick} {...props}>{text}</button>;
    }
}
```

### example.js
```js

// <button type="button">Click Me!</button>
ReactDOM.render(<Button>, el);

// Pass onButtonClick prop
const onButtonClick= () => alert('Clicked Me!');
ReactDOM.render(<Button handleClick={handleClick}>, el);
```
## Working with className
More than often you'll find yourself creating components that set a `className` on their rendered DOM element.

```js
class ButtonComponent extends Component {
    render() {
        return <button className="btn" {...this.props} />;
    }
}
```

This is fine and dandy:

```js
<ButtonComponent /> === <button className="button" />
```

Until you want to specify an additional `className` prop...

```js
<ButtonComponent className="blue" /> === <button className="button" />
<ButtonComponent className="blue" /> !== <button className="button blue" />
```

The component must be updated to handle `className` as intended. In this example, we intend to concatenate both class names together:

```jsx
class ButtonComponent extends Component {
    static propTypes = {
        className: PropTypes.string.isRequired
    };
    static defaultProps = {
        className: '' // If we did not provide a default value, render would need to check if undefined
    };
    render() {
        const { className, ...props } = this.props;
        const buttonClasses = 'btn ' + className;
        return <button className="btn" {...props} />;
    }
}
```

***This pattern can be applied to any prop, `className` is just used as an example here.***

## Working with className (Cont'd)
 
[classnames][0].
> a simple utility for conditionally joining classNames together.

Let's extend on the example above... 

1. Add `isClicked` prop to toggle the className "is-active"
2. Let's use [classnames][0] as it will help us here.

```js
import classNames from 'classnames'; // import module

class ButtonComponent extends Component {
    static propTypes = {
        className: PropTypes.string, // removed "isRequired" as classnames will handle undefined values
        isClicked: PropTypes.bool
    };
    static defaultProps = {
        isClicked: false // this line is optional, classnames will handle undefined values
    };
    render() {
        const { className, isClicked, ...props } = this.props;
        const classList = classNames('button', className, { 'is-active': isClicked });
        return <span className={classList} {...props} />;
    }
}
```

Now we have a configurable button...

```jsx
<ButtonComponent /> === <button className="button" />
<ButtonComponent isClicked={true} /> === <button className="button is-active" />
<ButtonComponent className="red" /> === <button className="button red" />
<ButtonComponent className="blink" isClicked={true} /> === <button className="button is-active blink" />
```
> ## CSS Modules
> [CSS Modules](https://github.com/css-modules/css-modules) are awesome. If you are not familiar with CSS Modules, it is a concept of using a module bundler such as [webpack](http://webpack.github.io/docs/) to load CSS scoped to a particular document. CSS module loader will generate a unique name for a each CSS class at the time of loading the CSS document ([Interoperable CSS](https://github.com/css-modules/icss) to be precise). To see CSS Modules in practice, [webpack-demo](https://css-modules.github.io/webpack-demo/).
> 
> In the context of React, CSS Modules look like this:
>
> ```js
> import React from 'react';
> import styles from './table.css';
> 
> export default class Table extends React.Component {
>     render () {
>         return <div className={styles.table}>
>             <div className={styles.row}>
>                 <div className={styles.cell}>A0</div>
>                 <div className={styles.cell}>B0</div>
>             </div>
>         </div>;
>     }
> }
> ```
> 
> Rendering the component will produce a markup similar to:
> 
> ```html
> <div class="table__table___32osj">
>     <div class="table__row___2w27N">
>         <div class="table__cell___2w27N">A0</div>
>         <div class="table__cell___1oVw5">B0</div>
>     </div>
> </div>
> ```
> 
> and a corresponding CSS file that matches those CSS classes.

Source: https://www.npmjs.com/package/react-css-modules#css-modules

## Working with styles
The `style` property accepts an object that maps to CSS styles. This will output inline style attribute on the generated DOM element.

```js
class MyComponent {
    render() {
        const styles = { backgroundColor: 'black', color: 'lime' };
        return <div style={styles}>Hello World!</div>;
    }
}
```

Styles can be dynamic based on the component's current properties.

```js
class MyComponent {
    static defaultProps = {
        bgColor: 'black',
        txtColor: 'lime'
    };
    render() {
        const { bgColor, txtColor } = this.props;
        const styles = { backgroundColor: bgColor, color: txtColor };
        return <div style={styles}>Hello World!</div>;
    }
}
```

Here is another example..

```js
class MyComponent {
    static defaultProps = {
        isBig: false
    };
    render() {
        const { isBig} = this.props;
        const styles = isBig ? { fontSize: '300%' } : null;
        return <div style={styles}>Hello World!</div>;
    }
}
```

[0]: https://www.npmjs.com/package/classnames

[0]: https://facebook.github.io/react/docs/reusable-components.html#es6-classes

[0]: https://facebook.github.io/react/docs/multiple-components.html#dynamic-children

[0]: https://github.com/DrkSephy/es6-cheatsheet#destructuring-objects

[0]: https://facebook.github.io/react/docs/reusable-components.html

### Gotchas

#### External SVG 

- When working with an SVG sprite file it is important to have the [namespace declaration](https://developer.mozilla.org/en-US/docs/Web/SVG/Namespaces_Crash_Course) in the file E.g

```xml
<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" class="sprite">
```       

- The SVG may not get rendered without the namespace in the opening tag

# Further reading  :

# React Notes 2

- To prevent syntax repetition you can abstract common properties from the React object using [ES6 Destructuring](https://github.com/DrkSephy/es6-cheatsheet#destructuring) E.g:

```js
//before
import React from 'react';

class Searchbar extends React.Component {
    static propTypes = {
        property1: React.PropTypes.string.isRequired,
        property2: React.PropTypes.any
    }
    static defaultProps = {
        property1: ''
    }
}

//after
import React, {Component, PropTypes} from 'react';

class Searchbar extends Component {
    static propTypes = {
        property1: PropTypes.string.isRequired,
        property2: PropTypes.any
    }
    static defaultProps = {
        property1: ''
    }
}
```

### Functional Component

- Similar to a function and returns `jsx` that gets rendered to the DOM

```js
//Searchbar.js
const Searchbar = () => {
    return <input />;
};

//index.js
const App = () => {
    return (
        <div>
            <Searchbar />
        </div>
    );
}
```
- In functional components the `props` object is passed as an argument E.g:

```js
const App = (props) => { }
```

### Class Component

- Used whenever a component needs to have some kind of internal record keeping

- It is self aware and keeps track of anything that happens to it once it has been rendered

- It is created using an [ES6 `class`](https://github.com/DrkSephy/es6-cheatsheet#classes)

```js
class Searchbar extends React.Component {
    render() {
        return <input />;
    }
}
```

- By extending `React.Component` you give the `Searchbar` class added functionality (state and props)

- To call an instance of a `class` you have to wrap it in jsx tags E.g: `<Searchbar />`

- Start off with a functional component and as your component gets complex you can convert to a class

- In a `class` component `props` are available within the component and don't need to be passed in as an argument. It can be accessed in a method using `this.props`

### Event Handling

- Similar to a regular event handler, in react it is a function that runs anytime an event occurs

- In react you declare the event handler then pass it to the element that you want to monitor for events

- It is considered best practice to begin the name of an event handler with `on` or `handle` E.g:

```js
class Searchbar extends React.Component {
    handleInputChange(e) {
        console.log(e.target.value);
    }
    render() {
        return <input onChange={this.handleInputChange()} />;
    }
}
```

### State

- `state` is a plain javascript object that is used to record and react to user events

- Each `class` based component has its own state object

- Whenever `state` is changed a component re-renders and also forces all of its children to re-render as well

- Before `state` can be used in a component the object needs to be initialized E.g:

```js
class Searchbar extends React.Component {
    constructor(props) {
        super(props);
        this.state = { term: ''};
    }
    handleInputChange(e) {
        console.log(e.target.value);
    }
    render() {
        return <input onChange={this.handleInputChange()}/>;
    }
}
```

- The `constructor` function is called whenever a new instance of a `class` is created

- It is reserved for setting up certain configurations in a `class` such as initializing variables, initializing state or binding event handler methods

- `super` is a reference to the `constructor` method on the React.Component `class` that is getting extended. This means that is has its own `constructor` function and so to reference it we have to use the `super` keyword

- In the code above `state` has been initialized E.g: `this.state = { property1: '' }`

- This syntax should only be used to declare state within the `constructor` function

- `this.setState()` should be used to manipulate state after it has been initialized E.g `this.setState({ property1: 'new state'});`

```js
class Searchbar extends React.Component {
    constructor(props) {
        super(props);
        this.state = { term: ''};
    }
    render() {
        return (
            <div>
                <input
                    value={this.state.term}
                    onChange={(e) => this.setState({term: e.target.value })} />
            </div>
        );
    }
}
```
- In the code above the value of the input has been set to the `state`

- This means that the component is declarative, the `state` determines how the data or UI is manipulated.

- When an action (or change) occurs the component is already aware through its change in `state` and then re-renders

### Downwards Data Flow

- The most parent component (App) should be responsible for handling and fetching data in a react app E.g

```js
class App extends Component {
    constructor(props) {
        super(props);

        this.state = { videos: []};

        YTSearch({key: API_KEY, term: 'react js'}, (videos) => {
            this.setState({ videos })
            //this.setSate({ videos: videos});
        });
    }
    render() {
        return (
            <div>
                <Searchbar />
                <VideoDetail />
                <VideoList />
            </div>
        );
    }
}
```
- In the code above the `YTSearch` method is used to return a list of videos to a react app and this information is going to be used by multiple components

- It makes sense to call that method on the `constructor` of the `App` component which is the parent in this case

- This also makes it possible for every instance of the `App` to have that `YTsearch` API method available

- To prevent syntax repetition you can make use of [ES6 property value shorthand](https://ponyfoo.com/articles/es6-object-literal-features-in-depth)

- E.g : In the code above when `this.setState()` is called within the callback function the `videos` arg (which is a variable) is the same as the initialized `state` (`this.state = { videos: []}`) so instead of repeating that variable you can use ES6 to set it as the current state: `this.setState({ videos })`

- That is the same as saying : `this.setState({ videos: videos})`

##### More Examples

```js
//js without ES6
function getCar(make, model, value ) {
    return {
        make: make ,
        model: model,
        value: value
    };
}

//with ES6
function getcar(make, model, value) {
    return {make, model, value};
}
```

#### Iterating Over Data

- It is considered best practice to avoid the use of `for` loops in react

- You should make use of built-in helpers such as the array `map` method E.g

```js
//ES5
var array = [1, 2, 3];
array.map(function(number) { return number * 2});

//ES6
let array = [1, 2, 3];
array.map((number) => { number * 2});
```

#### Working with Strings

- Make use of [ES6 template literals](https://github.com/DrkSephy/es6-cheatsheet#strings) to concatenate strings and values E.g:

```js
const VideoDetail = ({video}) => {
    // const video = props.video;

    const videoId = video.id.videoId;
    const url = `https://www.youtube.com/embed/${videoId}`;

    return (
        <iframe className="embed-responsive-item" src={url}></iframe>
    );
}
```

### Sources

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export

- https://github.com/ModuleLoader/es6-module-loader/wiki/Brief-Overview-of-ES6-Module-syntax

- http://www.2ality.com/2014/09/es6-modules-final.html

- https://addyosmani.com/writing-modular-js/

- https://facebook.github.io/react/docs/reconciliation.html

- http://facebook.github.io/react/docs/jsx-in-depth.html

- https://facebook.github.io/react/docs/thinking-in-react.html

- https://facebook.github.io/react/docs/top-level-api.html

- https://facebook.github.io/react/docs/reusable-components.html

- https://facebook.github.io/react/docs/glossary.html 