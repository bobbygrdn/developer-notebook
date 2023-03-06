# Overview

##### Create a Model of real-world objects using JavaScript objects that have both State and Behavior

<iframe width="548" height="308" src="https://www.youtube.com/embed/SS-9y0H3Si8" title="Software Development Tutorial - What is object-oriented language?" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

- Key Terms
  - State
  - Behavior
  - Property
  - Attribute
  - Method
- *State* refers to all of the data that your program holds onto in memory or other forms of data storage.
    - Each variable and it’s contents, along with any external systems that hold data constitutes the state of your program.
- *Behavior* refers to the interactivity of your program.
    - Each time a piece of data interacts with an automated decision(like *if statements* or *function calls*) or another piece of data, that is the *behavior* of your program.
- In Object Oriented Programming(OOP), our program’s *state* is contained entirely within objects as *properties*(referred to as attributes in OOP).
    - These objects can modify their own *state* through the use of *methods.*
- Here is a simple example:
```javascript
const list = {

  items: [],

  add: function (item) {
    this.items.push(item)
  }

}

list.items; // <= []
list.add("chips");
list.items; // <= ["chips"]
```

- The *items* is the *state* of the list. It contains the data for the object, under the property *items*. Our objects can hold multiple *properties* that contain *state*, because *state* is simply “the current values contained under any identifier”.
- *Add* is the *behavior* of this object. The *add* function does something - it *mutates* the *state* of the list. In this case, it changes the list’s *items property*. *Add* is a *method*.

### Function Vs. Method

- You may have noticed in the above example we referred to *add* as a *method*. Let’s explore the difference between a function and a *method*.
- A *method* is a function that is called on an object.
- When you call a function using the syntax `list.add()` you are calling the *add method* on the *list* object.
- Let’s look at a couple common *methods* that are used in JavaScript:
    - `array.push()`
    - `string.match()`
- You may or may not have seen these methods before - they all operate on the object they are being called on.
    - `array.push()` modifies the object it’s being called on my adding an element to the front of the array object.
    - `string.match()` inspects the object it’s being called on and performs a calculation where it compares the string to a created *regular expression*(*regex*) for similarities.
- These *methods* perform different tasks on the objects that they are called upon. These *methods* do not modify any other objects, nor do they perform tasks unrelated to their area of responsibility.

### The "This" Keyword

- Using the *this* keyword is quite simple. Think of it in this way:
    - When a *method* is called on an object, *this* inside the method refers to the object that is calling the *method*.
- Using the example we used above we can explore the *this* keyword.
```javascript
const list = {

  items: [],

  add: function (item) {
    this.items.push(item) // in here, `this` refers to `list`
  }

}

list.add("chips");
```
- We called the *add method* on the *list* object. So inside the *add method* *this* refers to *list*.
- Let’s create our first object with both *state* and *behavior*.
```javascript
// cow is the name of the object, weight is the property of cow and eat is a method     inside the cow object
var cow = {
    
    weight: 100,
    
    eat: function(poundsOfFood) {
        this.weight += poundsOfFood
    }
};

cow.eat(10); // Calling the eat method on cow using 10 as an input will return weight: 110
```

### Critical Thinking Challange
- Imagine you are building a calculator program. What classes, properties, and methods do you think you would need and why?