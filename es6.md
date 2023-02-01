### ES6 notes

- ECMAScript 6, created to standardize JavaScript
- classes (not prefered, use functions instead)
    - like function, but instead of using `function` to initiate it, we use `class` and properties are assigned inside a `constructor()` method
    - example:
    ```jsx
    // using class and class inheritance
    class Car {
        constructor (name) {
            this.brand = name;
        }
        // example of a function inside a class
        present() {
            return 'I have a ' + this.brand;
        }
    }
    // inherited class
    class Model extends Car {
        constructor (name, mod) {
            super(name); // by calling super(), method in the constructor method, we call the parent's constructor method and get access to the parent's properties and methods
            this.model = mod;
        }
        show () {
            return this.present() + ', it is a ' + this.model
        }
    }
    const mycar = new Car("ford")
    mycar.present(); //accesses the brandname of newly created Car object
    //inherited class
    const mycar = new Model("Ford", "mustang");
    mycar.show();    
    ```
- arrow functions:
    - example:
    ```jsx
    //before
    hello = function() {
        return "hello world";
    }
    //after
    hello = () => "hello world"; 
    //however works only if one statement
    ```
    - there is no binding of `this` in arrow function, [detail](https://www.w3schools.com/react/react_es6_arrow.asp)
        - usually `this` represents the object that called the function, which could be the window, the document, a button or whatever
        - with arrow functions, `this` keyword represents the object that defined the arrow function
- variables:
    - added in ES6, `let` and `const` (before only `var`)
        - `var` has a function scope
        - `let` has block scope
        - `const` variable never changes (assign only once)
- array methods:
    - `.map()` allows you to run a function on each item in the array
- destructuring:
    - example:
        ```jsx
        const vehicleOne = {
        brand: 'Ford',
        model: 'Mustang',
        type: 'car',
        year: 2021, 
        color: 'red',
        registration: {
            city: 'Houston',
            state: 'Texas',
            country: 'USA'
        }
        }
        myVehicle(vehicleOne)
        //interesting that you can directly access the values by key
        function myVehicle({ model, registration: { state } }) {
        const message = 'My ' + model + ' is registered in ' + state + '.';
        }
        ```
- modules:
    - allows your code to break into several files
    - example: on `message.js`
    ```jsx
    const message = () => {
    const name = "Jesse";
    const age = 40;
    return name + ' is ' + age + 'years old.';
    };
    ```
    - to import `message.js`
    - `import message from "./message.js";`
