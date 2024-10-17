Max score class implementation [source](https://www.geeksforgeeks.org/introduction-to-max-heap-data-structure/):

A Max-Heap is defined as a type of Heap Data Structure in which each internal node is greater than or equal to its children. A max-heap is always a complete binary tree and typically represented as an array. Note that unlike a normal binary tree, a complete binary tree can be represented as an array without wasting any memory.

The heap data structure is a type of binary tree that is commonly used in computer science for various purposes, including sorting, searching, and organizing data.


Purpose and Use Cases of Max-Heap:

- Priority Queue: One of the primary uses of the heap data structure is for implementing priority queues. 
- Heap Sort: The heap data structure is also used in sorting algorithms.  
- Memory Management: The heap data structure is also used in memory management. When a program needs to allocate memory dynamically, it uses the heap data structure to keep track of the available memory. 
- Graph Algorithms: The heap data structure is used in various graph algorithms. For example, Dijkstra’s shortest path algorithm uses a heap data structure to keep track of the vertices with the shortest path from the source vertex. 


A Max heap is typically represented as an array. 


- The root element will be at Arr[0]. 
- For any ith node Arr[i].
    - left child is stored at Arr[2*i+1] 
    - Right child is stored at Arr[2*i+2]
    - Parent is stored at at Arr[floor((i-1)/2)] (or Arr[(i-1)>>1])


**Advantages of Max-Heap Data Structure:**
- Efficiently maintain the maximum value: A max heap allows constant-time access to the maximum element in the heap, which makes it useful in applications where the maximum element needs to be found quickly.
- Efficient insert and delete operations: The insert and delete operations in a max heap have a time complexity of O(log n), which makes them efficient for large collections of elements.
- Priority Queues: A max heap can be used to implement a priority queue, which is useful in many applications such as job scheduling, task prioritization, and event-driven simulation.
- Sorting: A max heap can be used to implement heapsort, which is an efficient sorting algorithm that has a worst-case time complexity of O(n log n).
- Space efficiency: A max heap can be implemented as an array, which requires less memory compared to other data structures such as a binary search tree or a linked list.


```javascript

class MaxHeap {
    constructor() {
        this.heap = [];
    }

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

    remove() {
        if (this.heap.length ) {
            const item = this.heap[0];
            this.heap[0] = this.heap[this.heap.length - 1];
            this.heap.pop();
            this.heapifyDown();
            return item;
        }
    }

    add(item) {
        this.heap.push(item);
        this.heapifyUp();
    }

    heapifyUp() {
        let index = this.heap.length - 1;
        while (this.hasParent(index) && this.parent(index) < this.heap[index]) {
            this.swap(this.getParentIndex(index), index);
            index = this.getParentIndex(index);
        }
    }

    heapifyDown() {
        let index = 0;
        while (this.hasLeftChild(index)) {
            let largerChildIndex = this.getLeftChildIndex(index);
            if (this.hasRightChild(index) && this.rightChild(index) > this.leftChild(index)) {
                largerChildIndex = this.getRightChildIndex(index);
            }
            if (this.heap[index] > this.heap[largerChildIndex]) {
                break;
            } else {
                this.swap(index, largerChildIndex);
            }
            index = largerChildIndex;
        }
    }
}

```
_____________________________________________

### **Example 1**: Maximal Score After Applying K Operations


Problem: 
You are given a 0-indexed integer array nums and an integer k. You have a starting score of 0.

In one operation:

1. choose an index i such that 0 <= i < nums.length,
2. increase your score by nums[i], and
3. replace nums[i] with ceil(nums[i] / 3).

Return the maximum possible score you can attain after applying exactly k operations.
The ceiling function ceil(val) is the least integer greater than or equal to val.

Example 1:
    Input: nums = [10,10,10,10,10], k = 5
    Output: 50
    Explanation: Apply the operation to each array element exactly once. The final score is 10 + 10 + 10 + 10 + 10 = 50.


<details>
<summary>Solutions</summary>

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var maxKelements = function(nums, k) {
    const maxHeap = new MaxHeap();
    let maxScore = 0;

    for (let num of nums) {
        maxHeap.add(num);
    }
    
    while(k) {
        let val = maxHeap.remove();
        maxScore += val;
        maxHeap.add(Math.ceil(val / 3));
        k--;
    }

    return maxScore;
};

class MaxHeap {
    constructor() {
        this.heap = [];
    }

    getLeftChildIndex(parentIndex) { return 2 * parentIndex + 1; }
    getRightChildIndex(parentIndex) { return 2 * parentIndex + 2; }

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

    swap(indexOne, indexTwo) {
        const temp = this.heap[indexOne];
        this.heap[indexOne] = this.heap[indexTwo];
        this.heap[indexTwo] = temp;
    }

    peek() {
        if (this.heap.length === 0) {
            return null;
        }
        return this.heap[0];
    }

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

    add(item) {
        this.heap.push(item);
        this.heapifyUp();
    }

    heapifyUp() {
        let index = this.heap.length - 1;
        while (this.hasParent(index) && this.parent(index) < this.heap[index]) {
            this.swap(this.getParentIndex(index), index);
            index = this.getParentIndex(index);
        }
    }

    heapifyDown() {
        let index = 0;
        while (this.hasLeftChild(index)) {
            let largerChildIndex = this.getLeftChildIndex(index);
            if (this.hasRightChild(index) && this.rightChild(index) > this.leftChild(index)) {
                largerChildIndex = this.getRightChildIndex(index);
            }
            if (this.heap[index] > this.heap[largerChildIndex]) {
                break;
            } else {
                this.swap(index, largerChildIndex);
            }
            index = largerChildIndex;
        }
    }
}
```

