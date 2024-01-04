## Introduction
- a framework for building client applications in HTML, CSS, and JavaScript/TypeScript
- gives applications a clean structure
- includes a lot of re-usable code
- separation of concerns
- makes applications more testable

## Architecture
- Front-end 
  - UI, presentation 
- Back-end 
  - Data and Processing
- HTTP Services / APIs
  - endpoints that are accessible via the HTTP protocol


## Setting up
- install node
- `npm install -g @angular/cli`
- `ng new <project-name>`
  - creates a new project
  - do you need routing, Y (if you need different pages)
- `ng serve`
  - or `npm start`
    - this can be changed in the `package.json`
- `ng g c <name-of-component>` | `ng generate component <name-of-component>`
  - creates a component in `.`
- `ng g s <name-of-service>` | `ng generate service <name-of-component>`
  - creates a service in `.`
  - 
### Structure of the project
- `e2e` 
  - to write end to end tests for the application 
  - automated tests that simulate a user
- `node_modules`
  - all 3rd party libraries
- `src`
  - actual source code
  - `app`
    - components
    - modules
  - `assets`
    - image files/ text files/ icons
  - `environments`
  - `index.html`
  - `polyfills.ts`
    - features of javascript that angular needs
  - `styles.css`
  - `test.ts`
- `angular.json` | `.angular-cli.json` (old)
  - you can setup the `styles` here
  - for example, for setting up bootstrap
    - add `"node_modules/bootstrap/dist/css/bootstrap.min.css"` to `"styles"` list
    - add `"node_modules/bootstrap/dist/js/bootstrap.min.js"` to `"scripts"` list
- `.editorconfig`
  - settings for the editor
- `Karma.config.js`
  - test runner for javascript code
- `package.json`
- `protractor.config.js`
- `tsconfig.json`
  - how to compile the ts file
- `tslint.json`   

### Syntax
```ts
functionName(): Observable<any[]> { //functionName(): ReturnType

} 
```


### Files
#### `app-routing.module.ts`
```ts
Routes = [
  {
    path: 'path-to-use-in-the-url', // use '**' for default path 
    component: ComponentToLoad,
  },
  ...
]
```



## Parts

### Modules
- container for related components, services, directives
- keeps application modular and easy to manage
- root module is often called 'AppModule'

### Components
- `ng g c <name-of-component>`
- building blocks
- UI components (HTML, css) + [business logic](#business-logic)

### Templates
- used to define visual aspects of the application (presentation layer)
- promotes separation of layers; [business logic](#business-logic) (typescript) and UI presentation (HTML) into distinct parts
- can include bindings, directives
```ts
<div class="todo-item">
  <input type="checkbox" [checked]="isDone">
  <span>{{ taskName }}</span>
</div>
```

### Directives
- extends HTML's capabilities and enhance the behavior of your UI
- mechanism to create reusable, abstracted, and encapsulated behaviors within your templates
- `ngIf` -> conditional rendering
- `ngFor` -> generating list of elements
- `ngStyle`
- `ngClass`
- `ngModel` -> supports two-way data binding




### Services
- application logic that are not directly related to the UI
- code organization, reusability and maintainability
- same services could be used in multiple components
- includes 
  - business logic
  - authentication and authorization
  - caching and local storage management
  - error handling and logging

```ts
// pet.service.ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class PetService {
  private happinessLevel: number = 50; // Default happiness level
  getHappinessLevel(): number {
    return this.happinessLevel;
  }
  feedPet(): void {
    this.happinessLevel += 10; // Feeding increases happiness
  }
}
```

```ts
// pet.component.ts

import { Component } from '@angular/core';
import { PetService } from './pet.service';

@Component({
  selector: 'app-pet',
  template: `
    <h2>Your Pet's Happiness: {{ happiness }}</h2>
    <button (click)="feed()">Feed Pet</button>
  `
})
export class PetComponent {
  happiness: number;

  constructor(private petService: PetService) {
    this.happiness = this.petService.getHappinessLevel();
  }

  feed(): void {
    this.petService.feedPet();
    this.happiness = this.petService.getHappinessLevel();
  }
}
```

### Subsriptions
```ts
// example
export class HomeComponent implements OnInit{ //OnInit is a lifecycle hook
  productList: any [] = [];
  constructor (private productService: ProductService) {
    // only use constructors for initializations or property injections
  }
  ngOnInit(): void {
    // run api calls
    // handling input properties
    // setting up initial states
    this.loadAllProducts() //runs this function everytime the component is loaded
  }
  loadAllProducts() {
    this.productService.getAllProducts().subscribe((result: any) => {
      this.productList = result.data
    })
  }
}
```



### Routing
- route


### Angular Forms
- forms


### Pipes
- |
```ts
<p>The current temperature in {{ city }} is {{ temperature | number: '1.1-1' }}°C.</p>
```



### Modal
- display additional details or explanations without naviating away from the current context
- eg. are you sure you want to delete this item?
- or for data selection



###

#### Definitions

#### Business Logic
- refers to rules, calculation, algorithms, and processes that define how your application works and handles data
