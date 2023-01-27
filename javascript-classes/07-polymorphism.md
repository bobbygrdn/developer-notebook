# Polymorphism

- When **multiple** classes inherit from the same superclass, there are many interesting properties:
    - Each subclasses have a common `interface` , specifically that common interface is the instance variables and methods defined in the super class.
    - Each of the subclasses have the ability to override a method to provide special implementation while keeping the same interface.
- With this in mind, we can design functions that can take in instances of different classes (but share a common super class) and design for this common interface. The fancy term for this concept is `polymorphism`.
- Let’s us our building example. Here’s code on the Building class and its subclasses.

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

- Now, let’s create a function, `tallestBuilding`, which takes in an array of buildings (i.e. objects whose class inherits the Building class) and returns the building with the most floors.

```jsx
const tallestBuilding = function(buildings) {
  if (buildings.length === 0) {
    return null;
  }

  // Assume the tallest building is the first building
  let tallest = buildings[0];

  for (let i = 1; i < buildings.length; i++) {
    if (buildings[i].numberOfFloors > tallest.numberOfFloors) {
      tallest = buildings[i];
    }
  }

  return tallest;
}
```

- Notice that this function **only** checks for instance variables that were defined in the `Building` class (specifically `numberOfFloors`). This allows us to pass in **any** type of Building( Residential, Office, or even Building itself).

```jsx
const myHouse = new Residential(2, 1986, 4);
const empireState = new Office(102, 2014, 300);
const spaceNeedle = new Building(3, 1958);

const tallest = tallestBuilding([myHouse, empireState, spaceNeedle]);
console.log(tallest.numberOfFloors); // 102
console.log(tallest);                // Office object
```

- Let’s try another example. Let’s write a function called `generateInspectionList` that takes in an array of buildings, and only produces an array of buildings that need inspection.

```jsx
const generateInspectionList = function(buildings) {
  return buildings.filter((bldg) => {
    return bldg.needsInspection();
  });
}
```

- Again, the instance method needed (`needsInspection()`) is defined by the superclass, so each subclass has that method as well, so it will work for any building.

```javascript
const list = generateInspectionList([myHouse, empireState, spaceNeedle]);
console.log(list.length); // 2
console.log(list);        // [Residential, Building]
```