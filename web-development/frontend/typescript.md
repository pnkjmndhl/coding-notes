### Introduction
- superset of javascript (all javascript code is a valid typescript code)
- strong typing (optional)
- object oriented features
- compile-time errors
- great tooling options
- javascript donot understand typescript, so they have to be transpiled (compiled)

### Installing
- `npm install -g typescript`
- `tsc --version` to see the version
- `tsc <file-name>` compiles the typescript file and creates a js file


### Variable declarations
```ts
var number = 1; // a variable declared by a var keyword is always scoped to the nearest function
let count = 2; 
// also supported by ESC6
// scoped to nearest block 
```

### Types
```ts
let a: number;
let b: boolean;
let c: string;
let d: any;
let e: number [] = [1,2,3]
let f: any [] = [1,true, 'a', false]

const ColorRed = 0;
const ColorGreen = 1;
const ColorBlue = 2;

enum Color {Red, Green, Blue}; // Red = 0; Green = 1, Blue = 2
let backgroundColor = Color.Red;
```


#### Type Assertion
```ts
(<string>message).endsWith("c") //if the variable type is unknown to the compiler, and we want to access the intellicense
```

#### Arrow functions
```ts
let doLog = (message) => console.log(message);
```

#### Custom types
```ts
interface point { // purely for declaration
    x: number;
    y: number;
}


let drawPoint = (point) => { //inline annotations
    ///...

drawpoint ({
    x: 2;
    y: 3;
})
}
```

```ts
/// creating classes
class Point {
    x: number;
    y: number;

    draw() {
        // ...
    }

    getDistance (another: Point) {
        // ...
    }
}

let point = new Point();
point.draw();
```


#### Constructors
```ts
/// creating classes
class Point {
    x: number;
    y: number;

    constructor (x?: number, y?: number) { // x and y are optional because of ?
        this.x = x;
        this.y = y;
    }

    draw() {
        // ...
    }
}

let point = new Point(2,3);
point.draw();
```

##### Access modifiers
- public
- private
- protected


#### simplified form of class with access modifiers
```ts
/// creating classes
class Point {
    constructor (private x?: number, private y?: number) { // x and y are optional because of ?
    }

    draw() {
        // ...
    }
}

let point = new Point(2,3);
point.draw();
```