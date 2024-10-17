## Details

Radix Sort is a linear sorting algorithm that sorts elements by processing them digit by digit. It is an efficient sorting algorithm for integers or strings with fixed-size keys. [source](https://www.geeksforgeeks.org/radix-sort/?ref=previous_article)

#### Radix Sort Algorithm
The key idea behind Radix Sort is to exploit the concept of place value. It assumes that sorting numbers digit by digit will eventually result in a fully sorted list. Radix Sort can be performed using different variations, such as Least Significant Digit (LSD) Radix Sort or Most Significant Digit (MSD) Radix Sort.


Example to sort element

```javascript
//  Get maximum value in arr[]
function getMax(arr) {
  const length = arr.length;
  let mx = arr[0];

  for (let i = 1; i < length; i++) {
    if (arr[i] > mx) mx = arr[i];
  }
  return mx;
}

// A function to do counting sort of arr[] according to
// the digit represented by exp.
function countSort(arr, exp) {
  const length = arr.length;
  let output = Array(length); // output array
  let count = Array(10).fill(0, 0);

  // Store count of occurrences in count[]
  for (let i = 0; i < length; i++) {
    const digit = Math.floor(arr[i] / exp) % 10;
    count[digit]++;
  }

  // Change count[i] so that count[i] now contains
  // actual position of this digit in output[]
  for (let i = 1; i < 10; i++) {
    count[i] += count[i - 1];
  }

  // Build the output array
  for (let i = length - 1; i >= 0; i--) {
    const digit = Math.floor(arr[i] / exp) % 10;
    output[count[digit] - 1] = arr[i];
    count[digit]--;
  }

  return output;
}

// The main function to that sorts arr[] using Radix Sort
function radixSort(arr) {
  // Find the maximum number to know number of digits
  const maxNumber = getMax(arr);
  // Create a shallow copy where the sorted values will be kept
  let sortedArr = [...arr];

  // Do counting sort for every digit. Note that
  // instead of passing digit number, exp is passed.
  // exp is 10^i where i is current digit number
  for (let exp = 1; Math.floor(maxNumber / exp) > 0; exp *= 10) {
    // Get the Count sort iteration
    const sortedIteration = countSort(sortedArr, exp);
    sortedArr = sortedIteration;
  }

  return sortedArr;
}

const sortedArr = radixSort(arr);

```

Time Complexity: 

- Radix sort is a non-comparative integer sorting algorithm that sorts data with integer keys by grouping the keys by the individual digits which share the same significant position and value. It has a time complexity of O(d * (n + b)), where d is the number of digits, n is the number of elements, and b is the base of the number system being used.
- In practical implementations, radix sort is often faster than other comparison-based sorting algorithms, such as quicksort or merge sort, for large datasets, especially when the keys have many digits. However, its time complexity grows linearly with the number of digits, and so it is not as efficient for small datasets.


Space Complexity: 

- Radix sort also has a space complexity of O(n + b), where n is the number of elements and b is the base of the number system. This space complexity comes from the need to create buckets for each digit value and to copy the elements back to the original array after each digit has been sorted.