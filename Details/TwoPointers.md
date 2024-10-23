## Details
In many problems involving arrays or lists, we have to analyze each element of the array compared to its other elements.

To solve problems like these we usually start from the first index and loop through the array one or more times depending on our implementation. Sometimes, we also have to create a temporary array depending on our problem’s requirements.

The above approach might give us the correct result, but it likely won’t give us the most space- and time-efficient solution.

As a result, it is often good to consider whether our problem can be solved efficiently by using the two-pointers approach.


**In the two-pointer approach, pointers refer to an array’s indexes. By using pointers, we can process two elements per loop, instead of just one.**

Common patterns in the two-pointer approach involve:

- Two pointers each starting from the beginning and the end until they both meet
- One pointer moves at a slow pace while the other pointer moves at a faster pace
Both of the above patterns can help us to reduce the time and space complexity of our problems as we get the expected result in fewer iterations and without using too much additional space.

Now, let’s take a look at a few examples that will help us to understand this technique a bit better.

Two pointers is really an easy and effective technique that is typically used for searching pairs in a sorted array.
Given a sorted array A (sorted in ascending order), having N integers, find if there exists any pair of elements (A[i], A[j]) such that their sum is equal to X.


_____________________________________________

### **Example 1**: Sum Exists in an Array


Problem: Given a sorted array of integers, we need to see if there are two numbers in it such that their sum is equal to a specific value.

Example, if our input array is [1, 1, 2, 3, 4, 6, 8, 9] and the target value is 11, then our method should return true. However, if the target value is 20, it should return false.


<details>
<summary>Solutions</summary>
Naive solution:

```java
public boolean twoSumSlow(int[] input, int targetValue) {

    for (int i = 0; i < input.length; i++) {
        for (int j = 1; j < input.length; j++) {
            if (input[i] + input[j] == targetValue) {
                return true;
            }
        }
    }
    return false;
}
```

In the above solution, we looped over the input array twice to get all possible combinations. We checked the combination sum against the target value and returned true if it matches. The time complexity of this solution is O(n^2). 

Now let’s see how can we apply the two-pointer technique here:

```java
public boolean twoSum(int[] input, int targetValue) {

    int pointerOne = 0;
    int pointerTwo = input.length - 1;

    while (pointerOne < pointerTwo) {
        int sum = input[pointerOne] + input[pointerTwo];

        if (sum == targetValue) {
            return true;
        } else if (sum < targetValue) {
            pointerOne++;
        } else {
            pointerTwo--;
        }
    }

    return false;
}
```

Since the array is already sorted, we can use two pointers. One pointer starts from the beginning of the array, and the other pointer begins from the end of the array, and then we add the values at these pointers. If the sum of the values is less than the target value, we increment the left pointer, and if the sum is higher than the target value, we decrement the right pointer.

We keep moving these pointers until we get the sum that matches the target value or we have reached the middle of the array, and no combinations have been found. **The time complexity of this solution is O(n) and space complexity is O(1), a significant improvement over our first implementation. **
</details>




_____________________________________________

### **Example 2**: Rotate Array k Steps

Problem: Given an array, rotate the array to the right by k steps, where k is non-negative. 

Example, if our input array is [1, 2, 3, 4, 5, 6, 7] and k is 4, then the output should be [4, 5, 6, 7, 1, 2, 3].

<details>
<summary>Solutions</summary>
    We can solve this by having two loops again which will make the time complexity O(n^2) or by using an extra, temporary array, but that will make the space complexity O(n).

    Let’s solve this using the two-pointer technique instead:

```java
public void rotate(int[] input, int step) {
    step %= input.length;
    reverse(input, 0, input.length - 1);
    reverse(input, 0, step - 1);
    reverse(input, step, input.length - 1);
}

private void reverse(int[] input, int start, int end) {
    while (start < end) {
        int temp = input[start];
        input[start] = input[end];
        input[end] = temp;
        start++;
        end--;
    }
}
```

In the above methods, we reverse the sections of the input array in-place, multiple times, to get the required result. For reversing the sections, we used the two-pointer approach where swapping of elements was done at both ends of the array section.

Specifically, we first reverse all the elements of the array. Then, we reverse the first k elements followed by reversing the rest of the elements. **The time complexity of this solution is O(n) and space complexity is O(1).**

</details>



_____________________________________________

### **Example 3**: Middle Element in a LinkedList

Problem: Given a singly LinkedList, find its middle element. For example, if our input LinkedList is 1->2->3->4->5, then the output should be 3.

<details>
    <summary>Solutions</summary>

  We can also use the two-pointer technique in other data-structures similar to arrays like a LinkedList:    

  ```java
    public <T> T findMiddle(MyNode<T> head) {
        MyNode<T> slowPointer = head;
        MyNode<T> fastPointer = head;

        while (fastPointer.next != null && fastPointer.next.next != null) {
            fastPointer = fastPointer.next.next;
            slowPointer = slowPointer.next;
        }
        return slowPointer.data;
    }
  ```

  In this approach, we traverse the linked list using two pointers. One pointer is incremented by one while the other is incremented by two. When the fast pointer reaches the end, the slow pointer will be at the middle of the linked list. **The time complexity of this solution is O(n), and space complexity is O(1).**


</details>



_____________________________________________

### **Example 4**: Find all triplets with zero sum

Given an array of distinct elements. The task is to find triplets in the array whose sum is zero.

Example: 
```
Input: arr[] = {0, -1, 2, -3, 1}
Output: (0 -1 1), (2 -3 1)
Explanation: The triplets with zero sum are 0 + -1 + 1 = 0 and 2 + -3 + 1 = 0  

Input: arr[] = {1, -2, 1, 0, 5}
Output: 1 -2  1
Explanation: The triplets with zero sum is 1 + -2 + 1 = 0   
```

<details>
    <summary>Solutions</summary>
    
### **Naive approach:** Below is the idea to solve the problem

    Run three loops and check one by one whether the sum of the three elements is zero or not. If the sum of three elements is zero then print elements otherwise print not found.

  Follow the below steps to Implement the Idea: 

- Run three nested loops with loop counter i, j, k
- The first loops will run from 0 to n-3 and second loop from i+1 to n-2 and the third loop from j+1 to b. The loop counter represents the three elements of the triplet.
- Check if the sum of elements at i’th, j’th, k’th is equal to zero or not. If yes print the sum else continue.


```java
    static void findTriplets(int[] arr, int n) {
        boolean found = false;
        for (int i = 0; i < n - 2; i++) {
            for (int j = i + 1; j < n - 1; j++) {
                for (int k = j + 1; k < n; k++) {
                    if (arr[i] + arr[j] + arr[k] == 0) {
                        return true;
                    }
                }
            }
        }
    }
```

```javascript
    function findTriplets(arr) {
        const list = [];

        for (let i = 0; i < arr.length - 2; i++) {
            for (let j = i + 1; j < arr.length - 1; j++) {
                for (let k = j + 1; k < arr.length; k++) {
                    if (arr[i] + arr[j] + arr[k] === 0) {
                        list.push([arr[i], arr[j], arr[k]]);
                    }
                }
            }
        }

        return list;
   }
```

**Time Complexity**: O(n3), As three nested loops are required, so the time complexity is O(n3).
**Auxiliary Space**: O(1), Since no extra space is required, so the space complexity is constant.




### **Hashing approach:** Below is the idea to solve the problem

    This involves traversing through the array. For every element arr[i], find a pair with sum “-arr[i]”. This problem reduces to pair sum and can be solved in O(n) time using hashing.


Follow the steps below to implement the idea:

1. Create a HashSet to store a unique element.
2. Run a nested loop with two loops, the outer loop from 0 to n-2 and the inner loop from i+1 to n-1
3. Check if the sum of ith and jth element multiplied with -1 is present in the HashSet or not
4. If the element is present in the HashSet, print the triplet else insert the jth element in the HashSet.

```java
// Java program to find triplets in a given
// array whose sum is zero
import java.io.*;
import java.util.*;
 
class GFG {
 
    // function to print triplets with 0 sum
    static void findTriplets(int arr[], int n)
    {
        boolean found = false;
 
        for (int i = 0; i < n - 1; i++) {
            // Find all pairs with sum equals to
            // "-arr[i]"
            HashSet<Integer> s = new HashSet<Integer>();
            for (int j = i + 1; j < n; j++) {
                int x = -(arr[i] + arr[j]);
                if (s.contains(x)) {
                    System.out.printf("%d %d %d\n", x,
                                      arr[i], arr[j]);
                    found = true;
                }
                else {
                    s.add(arr[j]);
                }
            }
        }
 
        if (found == false) {
            System.out.printf(" No Triplet Found\n");
        }
    }
 
    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 0, -1, 2, -3, 1 };
        int n = arr.length;
        findTriplets(arr, n);
    }
}
 
// This code contributed by Rajput-Ji
```


```javascript

function findTriplets(arr, n) {
    const result = [];

    for (let i = 0; i < n - 1; i++) {
        const s = new Set();
        const oneElem = arr[i];

        for (let g = i + 1; g < n; g++) {
            const x = -(oneElem + arr[g]);

            if (s.has(x)) {
                result.push([
                    x,
                    oneElem,
                    arr[g]
                ])
            } else {
                s.add(arr[j]);
            }
        }
    }
 
    return result;
}
 
Input
    [0, -1, 2, -3, 1];

Output
-1 0 1
-3 2 1

```
Time Complexity: O(n2), Since two nested loops are required, so the time complexity is O(n2).
Auxiliary Space: O(n), Since a HashSet is required, so the space complexity is linear.



### **Sorting approach:** Below is the idea to solve the problem

    The idea is based on the above discussed approach using Hashmap of this post. For every element check that there is a pair whose sum is equal to the negative value of that element.


</details>







**Source:** 
https://www.geeksforgeeks.org/two-pointers-technique/
