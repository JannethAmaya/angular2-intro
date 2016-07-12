# Angular 2 - Intro

In this workshop we'll be building an Angular 2 app "El Menon de Oro" that allow users to:

* Give menon de oro to any Menon 
* Remove menon de oro from any menon who has one
* See all the menones that won menon de oro in the past

# The Angular CLI

One of the easiest ways to start a new Angular 2 application is to use the brand new Angular command-line interface (CLI) 
that allows you to create an application that already works, right out of the box and that follows the best practices.

This project was generated with [angular-cli](https://github.com/angular/angular-cli) version 1.0.0-beta.9.

## Install it!
To install angular CLI run the following in the terminal:
```bash
$ npm install -g angular-cli
```

##Generating our **Menon de Oro** app
```bash
$ ng new menon-de-oro
```
This will create a new directory for us with all the resources that we need to get started!

**Navigate to the new directory:**

```bash
$ cd menon-de-oro
```

Now, let's **start the dev server** with the followign command:
```bash
$ ng serve
```
**Awesome right?**

For our app we will need:
* Navbar and header
* Menon class
* Prize class (representing menon de oro)
* Menon service (to handle all the needed CRUD operations)

## Navbar and Header

Let's create a component to handle the navbar and header, run the following:
```bash
$ ng generate component header
```
This will create:
* src/app/header/header.component.css
* src/app/header/header.component.html
* src/app/header/header.component.spec.ts
* src/app/header/header.component.ts
* src/app/header/index.ts

Let's add our html in our component's view, please paste the following html in **header.component.html** :
```html
<!-- Header -->
<div id="header-wrapper">
   <div id="header">
      <!-- Logo -->
      <h1><a href="index.html">Menon de oro</a></h1>
      <!-- Nav -->
      <nav id="nav">
         <ul>
            <li class="current"><a href="index.html">Home</a></li>
            <li><a href="#">Premiados</a></li>
            <li><a href="#">Menones</a></li>
            <li><a href="#">Premiados Anteriores</a></li>
         </ul>
      </nav>
      <!-- Banner -->
      <section id="banner">
         <header>
            <h2>Bienvenido a Menon de Oro!</h2>
            <p>Aqui te damos tu premio! ( ͡ ° ͜ʖ  ͡͡ ° )</p>
         </header>
      </section>
   </div>
</div>
```

Now, go to **app.component.html** and replace its content with the following:
```html
<app-header></app-header>
```

serve the app and see our newly added header!

**it is not showing, right?**

OK, don't panic, we need to tell angular where to get things, in this case our app.component doesn't know about our header component, we need to tell it.
Go to the **app.component.ts** and replace its content with the following:
```javascript
import { Component } from '@angular/core';

import { HeaderComponent } from './header/header.component';

@Component({
  moduleId: module.id,
  selector: 'app-root',
  templateUrl: 'app.component.html',
  styleUrls: ['app.component.css'],
  directives: [ HeaderComponent ]
})
export class AppComponent {
 
}

```
it's working now!

## Menon Class

Let's create our Menon class, run the following:
```bash
ng generate class Menon
```

Replace the content with this:
```bash
export class Menon {
    id: number;
    name: string = '';
    gender: string = '';

  constructor(values: Object = {}) {
    Object.assign(this, values);
  }
}
```
The Angular CLI creates a spec file for every component/service/class it generates, let's see how we can test our angular 2 app.
Open the **menon.spec.ts** file and add the following unit test:
```javascript
it('should accept values in the constructor', () => {
    let menon = new Menon({
      name: 'Yesenia',
      gender: 'F'
    });
    expect(menon.name).toEqual('Yesenia');
    expect(menon.gender).toEqual('F');
  });
```
once you saved the file, run the following command:
```bash
ng test
```
## MenonService
The MenonService will handle all the logic of our app (we will store all the data in-memory for this workshop).

Generate the service, run:
```bash
ng generate service MenonService
```
