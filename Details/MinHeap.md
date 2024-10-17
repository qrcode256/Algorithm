A Min-Heap is defined as a type of Heap Data Structure in which each node is smaller than or equal to its children. 

The heap data structure is a type of binary tree that is commonly used in computer science for various purposes, including sorting, searching, and organizing data.


A Min heap is typically represented as an array. 



- The root element will be at Arr[0]. 
- For any ith node Arr[i]:
   -   Arr[(i -1) / 2] returns its parent node.
   -   Arr[(2 * i) + 1] returns its left child node.
   -   Arr[(2 * i) + 2] returns its right child node.


**Purpose and Use Cases of Min-Heap:**

- Implementing Priority Queue: One of the primary uses of the heap data structure is for implementing priority queues. 

- Dijkstra’s Algorithm: Dijkstra’s algorithm is a shortest path algorithm that finds the shortest path between two nodes in a graph. A min heap can be used to keep track of the unvisited nodes with the smallest distance from the source node.

- Sorting: A min heap can be used as a sorting algorithm to efficiently sort a collection of elements in ascending order.

- Median finding: A min heap can be used to efficiently find the median of a stream of numbers. We can use one min heap to store the larger half of the numbers and one max heap to store the smaller half. The median will be the root of the min heap.

[source in geeksforgeeks](https://www.geeksforgeeks.org/introduction-to-min-heap-data-structure/)


**Advantages of Min-heap Data Structure:**
- Efficient insertion and deletion: Min heap allows fast insertion and deletion of elements with a time complexity of O(log n), where n is the number of elements in the heap.
- Efficient retrieval of minimum element: The minimum element in a min heap is always at the root of the heap, which can be retrieved in O(1) time.
- Space efficient: Min heap is a compact data structure that can be implemented using an array or a binary tree, which makes it space efficient.
- Sorting: Min heap can be used to implement an efficient sorting algorithm such as heap sort with a time complexity of O(n log n).
- Priority Queue: Min heap can be used to implement a priority queue, where the element with the minimum priority can be retrieved efficiently in O(1) time.
- Versatility: Min heap has several applications in computer science, including graph algorithms, data compression, and database systems.


_____________________________________________

### **Example 1**: Kth Largest Element in an Array


Problem: 
Given an integer array nums and an integer k, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.

Can you solve it without sorting?

Example 1:
    Input: nums = [3,2,1,5,6,4], k = 2
    Output: 5

Example 2:
    Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
    Output: 4

<details>
<summary>Solutions</summary>

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */

class MinHeap {
    constructor() {
        this.heap = [];
    }
 
    size() {
        return this.heap.length;
    }

    // Helper Methods
    getLeftChildIndex(parentIndex) {
        return 2 * parentIndex + 1;
    }
    getRightChildIndex(parentIndex) {
        return 2 * parentIndex + 2;
    }
    getParentIndex(childIndex) {
        return Math.floor((childIndex - 1) / 2);
    }
    hasLeftChild(index) {
        return this.getLeftChildIndex(index) < this.heap.length;
    }
    hasRightChild(index) {
        return this.getRightChildIndex(index) < this.heap.length;
    }
    hasParent(index) {
        return this.getParentIndex(index) >= 0;
    }
    leftChild(index) {
        return this.heap[this.getLeftChildIndex(index)];
    }
    rightChild(index) {
        return this.heap[this.getRightChildIndex(index)];
    }
    parent(index) {
        return this.heap[this.getParentIndex(index)];
    }
 
    // Functions to create Min Heap
     
    swap(indexOne, indexTwo) {
        const temp = this.heap[indexOne];

        this.heap[indexOne] = this.heap[indexTwo];
        this.heap[indexTwo] = temp;
    }
 
    peek() {
        if (this.heap.length) {
            return this.heap[0];
        }
    }
     
    // Removing an element will remove the
    // top element with highest priority then
    // heapifyDown will be called 
    remove() {
        if (this.heap.length === 0) {
            return null;
        }
        const item = this.heap[0];
        this.heap[0] = this.heap[this.heap.length - 1];
        this.heap.pop();
        this.heapifyDown();
        return item;
    }
 
    add (item) {
        this.heap.push(item);
        this.heapifyUp();
    }
 
    heapifyUp () {
        let index = this.heap.length - 1;

        while (this.hasParent(index) && this.parent(index) > this.heap[index]) {
            this.swap(this.getParentIndex(index), index);
            index = this.getParentIndex(index);
        }
    }
 
    heapifyDown () {
        let index = 0;
        while (this.hasLeftChild(index)) {
            let smallerChildIndex = this.getLeftChildIndex(index);
            if (this.hasRightChild(index) && this.rightChild(index) < this.leftChild(index)) {
                smallerChildIndex = this.getRightChildIndex(index);
            }
            if (this.heap[index] < this.heap[smallerChildIndex]) {
                break;
            } else {
                this.swap(index, smallerChildIndex);
            }
            index = smallerChildIndex;
        }
    }
}
 

var findKthLargest = function(nums, k) {
    const minHeapQueue = new MinHeap();

    for (let i = 0; i <nums.length ; i++) {
        if (minHeapQueue.size() < k) {
            minHeapQueue.add(nums[i]);
        } else if (minHeapQueue.heap[0] < nums[i]){
            minHeapQueue.remove();
            minHeapQueue.add(nums[i]); 
        }
    }

    return minHeapQueue.remove();
};
```

</details>
