# Inheritance

- One of the amazing features of Object Oriented Programming is called `inheritance`. This allows the ability for a class to use instance variables and methods from another class. It is usually described as a child class inheriting instance variables and methods from a parent class. Alternatively, it can be described as a subclass inheriting instance variables and methods from a `super` class.
- In our building example, there are many types of buildings we may want to share instance variables and methods. Take an example of Residential buildings (aka your house) and Office Buildings (a building like Google Headquarters or the Empire State Building).

```jsx
class Building {
  constructor(numberOfFloors, yearLastInspected) {
    this.numberOfFloors = numberOfFloors;
    this.yearLastInspected = yearLastInspected;
    this.specialActionNeeded = false;
  }

  addFloor() {
    this.numberOfFloors += 1;
  }

  needsInspection() {
    return this.specialActionNeeded || new Date().getFullYear() - this.yearLastInspected > 10;
  }
}

class Residential extends Building {
  constructor(numberOfFloors, yearLastInspected, numberOfFamilies) {
    super(numberOfFloors, yearLastInspected);
    this.numberOfFamilies = numberOfFamilies;
  }

  familiesPerFloor() {
    return this.numberOfFamilies / this.numberOfFloors;
  }
}

class Office extends Building {
  constructor(numberOfFloors, yearLastInspected, numberOfOffices) {
    super(numberOfFloors, yearLastInspected);
    this.numberOfOffices = numberOfOffices;
  }

  addFloor() {
    super.addFloor();
    this.specialActionNeeded = true;
  }

  officesPerFloor() {
    return this.numberOfOffices / this.numberOfFloors;
  }
}
```

- We define the inheritance using the `extends` keyword where the subclass `extends`
 from the superclass. Doing so provides all of the constructor functionality as well as the instance variables: (`numberOfFloors`, `yearLastInspected`, `specialActionNeeded`, etc.).

### Super Keyword

- When inheriting a class, the subclass will have access to a new keyword, `super`. This references the superclass it is inheriting from. It can be used in two ways:
    - Invoking `super()` calls the constructor on the superclass. This ensures the initial values are set from a super class (See the constructors on `OfficeBuilding` and `ResidentialBuilding`). **Calling `super()` in the constructor is required in order to use** `this` **in the constructor.**
    - Calling `super.methodName()` allows the ability to call a method from the superclass specifically. This allows the ability to **override** methods while still being able to include the functionality from the superclass (See the `addFloor()` method of the `OfficeBuilding`).

### Extra Properties/Methods

- Each subclass of `Building` has an additional property with `numberOfFamilies` associating with a Residential building and `numberOfOffices` associating with an Office building. Each subclass of `Building` also has a custom method as well. Try the following out:

```javascript
const myHouse = new Residential(2, 1986, 4);
const empireState = new Office(102, 2014, 300);

console.log(myHouse.numberOfFloors);         // 2
console.log(myHouse.numberOfFamilies);       // 4
console.log(myHouse.familiesPerFloor());     // 2
console.log(myHouse.numberOfOffices);        // undefined

console.log(empireState.numberOfFloors);     // 102
console.log(empireState.numberOfOffices);    // 300
console.log(empireState.officesPerFloor());  // 2.94...
console.log(empireState.numberOfFamilies);   // undefined
console.log(empireState.needsInspection());  // false
console.log(empireState.addFloor());
console.log(empireState.numberOfFloors);     // 103
console.log(empireState.needsInspection());  // true
```