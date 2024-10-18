Allow to find quick find element in array


```javascript

// find first element greater than target
function binarySearch(nums, lower, higher, target) {
    while (lower < higher) {
        let mid = (lower + higher) >>> 1;

        if (nums[mid] <= target) {
            lower = mid + 1;
        } else {
            higher = mid;
        }
    }

    return lower;
}

```

_____________________________________________

### **Example 1**: Sum Exists in an Array

Given an int array nums of length n. Split it into strictly decreasing subsequences. Output the min number of subsequences you can get by splitting.



Example 1:
    Input: [5, 2, 4, 3, 1, 6]
    Output: 3
    Explanation:
        You can split this array into: [5, 2, 1], [4, 3], [6]. And there are 3 subsequences you get.
        Or you can split it into [5, 4, 3], [2, 1], [6]. Also 3 subsequences.
        But [5, 4, 3, 2, 1], [6] is not legal because [5, 4, 3, 2, 1] is not a subsuquence of the original array.

Example 2:
    Input: [2, 9, 12, 13, 4, 7, 6, 5, 10]
    Output: 4
    Explanation: [2], [9, 4], [12, 10], [13, 7, 6, 5]

Example 3:
    Input: [1, 1, 1]
    Output: 3
    Explanation: Because of the strictly descending order you have to split it into 3 subsequences: [1], [1], [1]


<details>
<summary>Solutions</summary>

```javascript
(function main() {
    // find first element greater than target
    function binarySearch(nums, lo,  hi, target) {
        while (lo < hi) {
            let mid = (lo + hi) >> 1;
            if (nums[mid] <= target) {
                lo = mid + 1;
            } else {
                hi = mid;
            }
        }
        
        return lo;
    }
    
     function leastSubsequences(...nums) {
        const piles = new Array(nums.length);
        let size = 0;
        for (let num of nums) {
            let pile = binarySearch(piles, 0, size, num);
            piles[pile] = num;
            if (pile == size) size++;
        }
        return size;
    }
    
    function test(actual, expected) {
        if (actual == expected) {
            console.log("PASSED! ");
        } else {
            console.log(`FAILED! Expected ${expected}, but got ${actual}`);
        }
    }
    
    
    test(leastSubsequences(2, 9, 12, 13, 4, 7, 6, 5, 10), 4);
    test(leastSubsequences(5, 2, 4, 3, 1, 6), 3);
    test(leastSubsequences(1, 1, 1), 3);    
}());
```
</details>