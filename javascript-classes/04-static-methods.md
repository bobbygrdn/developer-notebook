# Static Methods

### Creating Static Methods

- Static methods are functions that are related to a class but are not related to an individual instance of a class. This may seem like an odd thing to do, but you've likely already seen static methods like the following:

```jsx
Math.random()
Array.isArray('not an array')
Object.keys({ color: 'red' })
```

- In the above example, the `.isArray()` method would not make sense to call on the string — or every other type for that matter. `Array.isArray` handles array-like functionality but is not related to a specific array.

[MDN: Static Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#Static_methods)