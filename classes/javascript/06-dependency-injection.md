# Dependency Injection

### Instances with Instances

- In the previous lessons we created instances as defined by a Class as well as defined properties and behavior on that Class using instance variables and methods. Since an instance is just an object we can use it in the same way we use any other object, including adding it to an array or even setting it to an instance variable of another class.

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

class City {
  constructor(name) {
    this.name = name;
    this.buildings = [];
  }

  addBuilding(building) {
    this.buildings.push(building);
  }

  addFloorToAllBuildings() {
    this.buildings.forEach(building => building.addFloor());
  }
}

const newYork = new City('New York City');
const empireState = new Building(102, 2014);

newYork.addBuilding(empireState);
newYork.addFloorToAllBuildings(); // Empire State Building gains a floor

const freedomTower = new Building(104, 2015);
newYork.addBuilding(freedomTower);
newYork.addFloorToAllBuildings(); // Both buildings gain a floor
```

- In this case, the `City` class uses the methods of `Building` to implement some new functionality. When we have various object instances interacting with each other like this, we can use the term `dependency injection`. This refers to the face that the new instance (e.g. a `City` instance) depends upon functionality from an instance of another class (e.g. the `Building` class).