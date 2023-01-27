# Binary Search

### Explanation:
- Binary Search takes in a sorted list of elements.
- Reduces the list by half everytime the algorithm runs.
- Starts in the middle of the list using that value as a reference.
- Returns the index of the value if the value is in the array
- Returns none if the value is not in the array 

### Code Snippet

```javascript
const binarySearch = (array, item) => {
	let low = 0;
	let high = array.length-1;

	while (low <= high) {
		let mid = Math.floor((low + high) / 2);
		let guess = array[mid];
		if (guess == item) {
			return mid;
		}
		if(guess > item) {
			high = mid -1;
		} else {
			low = mid + 1;
		}
	}
	return none;
}
```

### Process

```javascript
// Binary Search takes in a sorted array and an item to search for
const binarySearch = (array, item) => {
	// We assign the low variable to zero
	let low = 0;
	// We assign the high variable to the length of the list - 1
	let high = array.length-1

	/* We initiate a while loop that will run until the low variable isn't lower or equal
	to the high variable */
	while (low <= high) {

		/* We add the low value to the high value and divide them by two to get the middle
		index and assign it to the mid variable */
		let mid = Math.floor((low + high) / 2);
		
		/* We take the value of mid and use it to point to the middle element in the array
		and assign it to the guess variable, which is our current guess to see if the
		element is in the array */
		let guess = array[mid];

		/* We check to see if our guess matches the item we are searching for and if it is
		we return the value of mid which is the index location of where that item is in our
		array */
		if (guess == item) {
			return mid;
		}
			
		/* if guess is higher than the item we are looking for we reassign our high variable
		to the index of mid -1 or the index right before mid */
		/* if guess is lower than the item we are looking for we reassign our low variable
		to the index of mid +1 or the index right after mid */
		if(guess > item) {
			high = mid -1;
		} else {
			low = mid + 1;
		}
	}

	// if the while loop ends without finding the value in the array we return none
	return none;
}
```

### Example

```javascript
const binarySearch = (array, item) => {
	let low = 0;
	let high = array.length-1;

	while (low <= high) {
		let mid = (low + high) / 2;
		let guess = array[mid];
		if (guess == item) {
			return mid;
		}
		if(guess > item) {
			high = mid -1;
		} else {
			low = mid + 1;
		}
	}
	return none;
}

binarySearch([1,3,4,5,7,8,9], 5); //-> returns the index of the value which is 3
binarySearch([1,4,6,7,8,9,9], 2); //-> returns none because the value isn't in the array
```