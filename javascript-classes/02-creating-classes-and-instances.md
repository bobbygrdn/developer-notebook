# Creating Classes & Instances

### Key Terms

- Class
- Constructor Function
- Instance
- ES6
- Class Keyword

### What is an instance?

- Oftentimes we view many real objects that have a common template. For example, what does your house (or apartment complex), the Empire State building, and Smith Tower have in common? They are all buildings and have similar features including a foundation, a set of doors and windows, etc. A `class` is a template used to generate independent JavaScript objects.

```jsx
class Building {

}
// This is an example of a basic Building class
```

- To generate the independent JavaScript objects, we use the keyword `new` . The process is know as `instantiation` and the objects created become `instances`.

```jsx
const myHouse = new Building();
const empireState = new Building();
const smithTower = new Building();
```

- Instances share the same template known as a `class`. These instances can have properties — or `instance` variables — that are created for all `instances` of the class. An instance variable can be set with a default value or have the value set dynamically per instance.

### Instance Variables

- Below we are setting both a default value for a `hasEmergencyExit` instance variable and setting a dynamic value for a `numberOfFloors` instance variable.

```jsx
class Building {
	constructor(floors) {
		this.numberOfFloors = floors;
		this.hasEmergencyExit = true;
	}
}

const myHouse = new Building(2);
const empireState - new Building(102);

console.log(myHouse.numberOfFloors);       // 2
console.log(myHouse.hasEmergencyExit);     // true
console.log(empireState.numberOfFloors);   // 102
console.log(empireState.hasEmergencyExit); // true
```

- Each class has the ability to specify a `constructor`, a function that is invoked upon `instantiation` — when an instance is created. The constructor can take arguments which would be specified upon instantiation with `new`.
- Notice the use of the variable `this`. The `this` keyword references the new instance being created, not the class. This allows us to specify a variable (in this case `numberOfFloors`) on each individual building instance.

### Instance Methods

- We also have the ability to add functions on each instance, called `methods` . In essence, an `instance method` is a function assigned to an instance variable. These methods allow an instance to have behavior based on the properties defined in our instance variables. A method is able to have the same reference to the `this` variable in its definition. Let's continue our example with buildings.

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
const myHouse = new Building(2, 1986);       // 2 floors inspected in 1986

console.log(empireState.numberOfFloors);     // 102
console.log(myHouse.numberOfFloors);         // 2

// My House needs to expand another floor
myHouse.addFloor();
console.log(empireState.numberOfFloors);     // 102 (No Change)
console.log(myHouse.numberOfFloors);         // 3

if (myHouse.needsInspection()) {
  console.log('My House Needs Inspection');  // Will get printed
}
```

### Recap With More Examples

- To create classes with the class keyword, you’ll have three parts:
    - Class  name: class `NameOfYourClass { … }`, then within the class body:
        - Constructor Function: `constructor(a,b,c) { … }`
        - Methods: `myMethod(a,b) { … }`
- Let’s look at a few examples:

```jsx
// CLASS NAME
class Dog { 

  // CONSTRUCTOR FUNCTION
  constructor(name, breed, address, age) {
    this.name = name;
    this.breed = breed;
    this.address = address;
    this.age = age;
  }

  //METHODS
  speak() {  
     var sounds = ["bark", "grrrrrr", "rough rough", "woof", "oink"];
     var rand = Math.floor(Math.random() * sounds.length);
     return this.name + " says " + sounds[rand];
  };

} // Constructor Function, and instance methods are within the class body

// Usage remains the same
var moxie = new Dog("moxie", "Manx", "1355 Market St #900", 5);
var deli = new Dog("Deli", "Labradoodle", "88 Colin P Kelly Jr St", 2);

console.log(moxie.speak()) // "moxie says (Random string from the array)"

console.log(deli.speak()) // "Deli says (Random string from the array)"

console.log(moxie.speak === deli.speak); 
// returns true, because we are re-using the same function across all instances of Dog
```

- Basic Example:

```jsx
// CLASS CREATION
class Vehicle {
  constructor(name, color){
    this.name = name;
    this.color = color;
  }

  honk(){
    return `beep beep`
  }

}

// INSTANCE CREATION & USAGE
var oldCar = new Vehicle('Salvaged Car','faded red');

console.log(oldCar.name); // 'Salvaged Car'
console.log(oldCar.color); // 'faded red'
console.log(oldCar.honk()); // 'beep beep'
```

- Example with `this` keyword and parameters in method:

```jsx
// CLASS CREATION
class Tractor {
  constructor(name, color){
    this.name = name;
    this.color = color;
  }

  tow(trailer){
    return `${this.name} proceeds to tow ${trailer}`
  }

}

// INSTANCE CREATION & USAGE
var oldTractor = new Tractor('Salvaged Tractor','faded blue');

console.log(oldTractor.tow('old trailer')); "Salvaged Tractor proceeds to tow old       trailer"
```

- Example with properties set different ways in the constructor:

```javascript
// CLASS CREATION
class SpaceShip {
  constructor(name, shipclass, color, thrusters){
    // notice how we are combining parameters here to make "fullname"
    this.fullname = `${name}, ${shipclass}`;

    this.color = color;

    // If no argument is provided for "thrusters" when an instance of SpaceShip
    // is created, it will be undefined. If this happens, the OR operator "||" will     return 
    // what's on the right side as a default value. Otherwise if 
    // "thrusters" is defined, it will use the argument provided instead.
    this.thrusters = thrusters || {fullBurn: "Max Fuel Flow", cruise: "Light Full Flow"};
  }

  launch(){
    return `Launching with ${this.applyMaxForce()}`
  }

  applyMaxForce(){
    return this.thrusters.fullBurn;
  }

  cruise(){
    return this.cruise;
  }
}

// INSTANCE CREATION & USAGE
var planetExpress = new SpaceShip("Planet Express", "Delivery", "green");
console.log(planetExpress.launch()); // "Launching with Max Fuel Flow"

// INSTANCE CREATION & USAGE
var spaceXThruster = {fullBurn: "Ludicrious Speed, Go!", cruise: "Zzzzz"}
var spaceXship = new SpaceShip("spaceXship", "Spectacle", "silver", spaceXThruster);
console.log(spaceXship.launch()); // "Launching with Max Fuel Flow"
```