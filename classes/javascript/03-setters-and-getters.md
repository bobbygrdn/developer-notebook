# Setters & Getters

### Encapsulation

- Another important Object Oriented Programming (OOP) principle is `encapsulation`.
- Encapsulation is defined by two concepts:
    - Restricted access to instance variables and methods that do not need to be exposed.
    - Constructing methods to allow access to those instance variables and methods.

### Why is it important?

- Each instance is managing its own variables and methods. It’s often not a good idea for allowing the variables to be manipulated outside of the object itself.
- See an example of the buildings below:

```jsx
class Building {
  constructor(numberOfFloors, yearLastInspected) {
    this.numberOfFloors = numberOfFloors;
    this.yearLastInspected = yearLastInspected;
  }

  addFloor() {
    this.numberOfFloors += 1;
  }

  needsInspection() {
    return new Date().getFullYear() - this.yearLastInspected > 10;
  }
}

const empireState = new Building(102, 2014); // 102 floors inspected in 2014
empireState.numberOfFloors = 2;              // Godzilla visited New York City
console.log(empireState.numberOfFloors);     // 2
```

- In this case, `numberOfFloors` is something  that the `Building` class should only manage.

### How do we restrict instance variables and methods?

- Many languages allow the ability to restrict access on instance variables and methods, but unfortunately JavaScript does not have these features. The get around this limitation, developers have implemented the convention that deliberately restricted instance variables and methods should be preceded with an `_`.

```jsx
class Building {
  constructor(numberOfFloors, yearLastInspected) {
    this._numberOfFloors = numberOfFloors;
    this._yearLastInspected = yearLastInspected;
  }

  addFloor() {
    this._numberOfFloors += 1;
  }

  needsInspection() {
    return new Date().getFullYear() - this._yearLastInspected > 10;
  }
}

const empireState = new Building(102, 2014); // 102 floors inspected in 2014
```

- While we can specifically access `_numberOfFloors` and `_yearLastInspected`, it’s more explicit that the variables are not meant to be touched.

### Constructing Methods to Allow Access

- The second concept in encapsulation is constructing methods to get or set these values where necessary. The common approach is to specify methods of the name `getVariableName()` and `setVariableName(newValue)` . These respectively have been called `getters` and `setters` or `accessors` and `mutators`.

```jsx
class Building {
  constructor(numberOfFloors, yearLastInspected) {
    this._numberOfFloors = numberOfFloors;
    this._yearLastInspected = yearLastInspected;
  }

  getNumberOfFloors() {
    return this._numberOfFloors;
  }

  getYearLastInspected() {
    return this._yearLastInspected;
  }

  setYearLastInspected(newValue) {
    this._yearLastInspected = newValue;
  }

  addFloor() {
    this._numberOfFloors += 1;
  }

  needsInspection() {
    return new Date().getFullYear() - this._yearLastInspected > 10;
  }
}

const empireState = new Building(102, 2014);         // 102 floors inspected in 2014
console.log(empireState.getNumberOfFloors());        // 102
console.log(empireState.getYearLastInspected());     // 2014
empireState.setYearLastInspected(2016);
console.log(empireState.getYearLastInspected());     // 2016
```

### But I Like Variables!

- Tire of invoking methods and calling them to get/set information? No worries! ES6 offers the ability to specify the getters and setters specially.

```jsx
class Building {
  constructor(numberOfFloors, yearLastInspected) {
    this._numberOfFloors = numberOfFloors;
    this._yearLastInspected = yearLastInspected;
  }

  get numberOfFloors() {
    return this._numberOfFloors;
  }

  get yearLastInspected() {
    return this._yearLastInspected;
  }

  set yearLastInspected(newValue) {
    this._yearLastInspected = newValue;
  }

  addFloor() {
    this._numberOfFloors += 1;
  }

  needsInspection() {
    return new Date().getFullYear() - this._yearLastInspected > 10;
  }
}

const empireState = new Building(102, 2014);  // 102 floors inspected in 2014
console.log(empireState.numberOfFloors);       // 102
console.log(empireState.yearLastInspected);    // 2014
empireState.yearLastInspected = 2016;
console.log(empireState.yearLastInspected); // 2016
```

- Here is another example with getter and setter methods:

```javascript
class Library {
  constructor(name){
    this.name = name;

    // the underscore on "_books", is to avoid name confusion later
    // and denote that this is not meant to be accessed directly
    // it does not do anything special
    this._books = []; 

  }

  // You will see how this "get" method is used further down.
  get books(){ //notice the "get" keyword before books.

    // As you can see here, it allows us to send back a property 
    // with a certain formatting (in this case, the array is joined). 
    return this._books.join()

    // We could accomplish this with regular methods too, but the "get" keyword
    // allows us to access "books" from our instance as if it was a property
    // instead of a method. (see example on the instance further down)
  }

  // Similar to "get"
  set books(newBook){
    this._books.push(newBook);
  }


}

// INSTANCE CREATION & USAGE
var austinLibrary = new Library("Austin Library");

// SETTER USAGE: 
// With `set books(newBook){ ... }`, defined in our class,
// Instead of invoking it like this "instance.books()"
// we can use "instance.books = ...", and it will run the "books" method.
austinLibrary.books = "Where is Waldo?"; // runs set books(...), pushes string in to "instance._books"
austinLibrary.books = "Where is Carmen?"; // runs set books(...), pushes string in to "instance._books"

// GETTER USAGE:
// This will run "get books()"
console.log(austinLibrary.books) // "Where is Waldo?,Where is Carmen?"
```

<iframe width="685" height="385" src="https://www.youtube.com/embed/nx6DFeNIXlA" title="JavaScript 6 04:  Getters and Setters" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>