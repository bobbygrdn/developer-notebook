# Selection Sort

### Explanation:
- Selection Sort takes in an unsorted array
- Sorts the elements in the array and returns a sorted array

### Code Snippet

```javascript
const selectionSort = (array) => {
	newArray = [];
	while (array.length != 0) {
		let smallest = array[0];
		let smallest_index = 0;
		for (let i = 0; i < array.length; i++) {
			if (array[i] < smallest) {
				smallest = array[i];
				smallest_index = i;
			}
		}
		newArray.push(array.splice(smallest_index, 1))
	}
	return newArray.flat();
}
```

### Process

```javascript
// Selection Sort takes in an unsorted array
const selectionSort = (array) => {
	
	// We create an empty array to push elements into
	newArray = [];
	
	// We initialize a while loop that will end once our input array is empty
	while (array.length != 0) {

		/* We take the value of the element at index zero in the current array and assign it 
		to the smallest variable */
		let smallest = array[0];

		// We assign the number 0 to the smallest_index variable
		let smallest_index = 0;

		// We initialize a for loop that will loop over the length of our current array
		for (let i = 0; i < array.length; i++) {

			/* if the element at index zero in the array is smaller than the element that is 
			assigned to the smallest variable we assign the value of the array at the current 
			index to the smallest variable and we assign the value of i to the smallest_index 
			variable */
			if (array[i] < smallest) {
				smallest = array[i];
				smallest_index = i;
			}
		}
		/* Once the for loop finds the smallest element we splice that element off of the in
		put array and push it into our new array */
		newArray.push(array.splice(smallest_index, 1))
	}
	/* Once we have taken all the elements from the input array and pushed them into our 
	new array we return a flattened version of that array */
	return newArray.flat();
}
```

### Example 

```javascript
const selectionSort = (array) => {
	newArray = [];
	while (array.length != 0) {
		let smallest = array[0];
		let smallest_index = 0;
		for (let i = 0; i < array.length; i++) {
			if (array[i] < smallest) {
				smallest = array[i];
				smallest_index = i;
			}
		}
		newArray.push(array.splice(smallest_index, 1))
	}
	return newArray.flat();
}

selectionSort([6,4,8,9,3,5]) //-> Returns [3,4,5,6,8,9]
selectionSort([4,5,8,1,9,3,6]) //-> Returns [1,3,4,5,6,8,9] 
```