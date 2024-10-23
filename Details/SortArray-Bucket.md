## Details
[Source](https://www.geeksforgeeks.org/bucket-sort-2/)

Bucket sort as bin sort, is a sorting algorithm that divides elements into several buckets. The buckets are then sorted one at a time using a different sorting algorithm or by recursively use the bucket sorting. **Mostly used to sort ditigs**

The bucket sort method:
- Create an array of "buckets" that are initially empty
- Scatter: Go through the original array, placing each object in its appropriate bucket
- Each non-empty bucket should be sorted
- Gather: Return all elements to the original array after visiting the buckets in order


### Complexity:
#### Time complexity

Average Case Complexity O(n + k)

- It happens when the array's elements are distributed at random.
- Bucket sorting takes linear time, even if the elements are not distributed uniformly. 
- It holds until the sum of the squares of the bucket sizes is linear in terms of the total number of elements.

Worst Case Complexity O(n * n)

- When elements in the array are close in proximity, they are likely to be placed in the same bucket. 
- As a result, some buckets may contain more elements than others. 
- It makes the complexity dependent on the sorting algorithm used to sort the bucket's elements.
- When the elements are placed in reverse order, the complexity increases even more.
- When insertion sort is used to sort bucket elements, the time complexity becomes O (n2).


#### Space complexity

The space complexity is O(n+k).


### Variation bucket sort:
 - Proxmap Sort - similar to hashing. It divides an array of keys into subarrays using a "map key" function that preserves a partial ordering on the keys; as each key is added to its subarray, insertion sort is used to keep that subarray sorted, resulting in the entire array being in sorted order when ProxmapSort finishes.
 
 - Generic Bucket Sort

_____________________________________________

### **Example 1**: Sort number array


Problem: Given an array of numbers, we need to sort the array

Example, our array is [6, 1, 8, 2, 4, 1, 9, 3] the output is [1, 1, 2, 3, 4, 6, 8, 9] 

<details>
<summary>Solutions</summary>

```javascript
function insertionSort(bucket) {
    for (let i = 1; i < bucket.length; ++i) {
        let key = bucket[i];
        let j = i - 1;

        while (j >= 0 && bucket[j] > key) {
            bucket[j + 1] = bucket[j];
            j--;
        }
        bucket[j + 1] = key;
    }
}

function bucketSort(arr) {
    let n = arr.length;
    let buckets = Array.from({length: n}, () => []);

    // Put array elements in different buckets
    for (let i = 0; i < n; i++) {
        let bi = Math.floor(n * arr[i]);
        buckets[bi].push(arr[i]);
    }

    // Sort individual buckets using insertion sort
    for (let i = 0; i < n; i++) {
        insertionSort(buckets[i]);
    }

    // Concatenate all buckets into arr[]
    let index = 0;

    for (let i = 0; i < n; i++) {
        for (let j = 0; j < buckets[i].length; j++) {
            arr[index++] = buckets[i][j];
        }
    }
}

let arr = [0.897, 0.565, 0.656, 0.1234, 0.665, 0.3434];
bucketSort(arr);
```

</details>