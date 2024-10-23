### **Basics of Bit Manipulation**
 
Understanding the core bitwise operators is essential for solving bit manipulation problems.

- **AND (`&`)**: Masks bits, used to clear bits or check specific bits.
- **OR (`|`)**: Sets specific bits in a number.
- **XOR (`^`)**: Flips bits when two bits are different, used for toggling bits or checking equality.
- **NOT (`~`)**: Inverts all bits.
- **Left Shift (`<<`)**: Multiplies by powers of two.
- **Right Shift (`>>`)**: Divides by powers of two.
- **Key Concept**: Understanding how these operators work on binary representations of numbers.

**Examples**:

| TITLE                                         | LEVEL    | SOURCE |  
| -----                                         | ----     | ----   |
| #191. Number of 1 Bits                        |  Easy    |  https://leetcode.com/problems/number-of-1-bits/description/  |
| #231. Power of Two                            |  Easy    |  https://leetcode.com/problems/power-of-two/                  |
| #136. Single Number                           |  Easy    |  https://leetcode.com/problems/single-number/                 |
| #268. Missing Number                          |  Easy    |  https://leetcode.com/problems/missing-number/                |
| #190. Reverse Bits                            |  Easy    |  https://leetcode.com/problems/reverse-bits/                  |
| #371. Sum of Two Integers                     |  Medium  |  https://leetcode.com/problems/sum-of-two-integers            |
| #191.Number of 1 Bits                         |  Easy    |  https://leetcode.com/problems/number-of-1-bits               |
| #268. Missing Number                          |  Easy    |  https://leetcode.com/problems/missing-number                 |
| #190. Reverse Bits                            |  Easy    |  https://leetcode.com/problems/reverse-bits                   |
| Counting Bits                                 |  Easy    |  https://leetcode.com/problems/counting-bits                  |
| Check whether K-th bit is set or not          |  Easy    |  https://www.geeksforgeeks.org/check-whether-k-th-bit-is-set-or-not/   |
| Check if a number is odd or even              |  Easy    |  https://www.geeksforgeeks.org/program-to-check-even-or-odd/           |
| Toggle K-th bit                               |  Easy    |  https://www.geeksforgeeks.org/toggle-k-th-bit-given-number/           |

---

### **Power of Two Checks**
- To check if a number `n` is a power of two, use `n & (n - 1)`. If the result is `0`, it’s a power of two. Powers of two have only one bit set in their binary representation.

**Examples**:

| TITLE                                               | LEVEL    | SOURCE |  
| -----                                               | ----     | ----   |
| #231. Power of Two                                  |  Easy    |  https://leetcode.com/problems/power-of-two/        |
| #342. Power of Four                                 |  Easy    |  https://leetcode.com/problems/power-of-four/       |
| #326. Power of Three                                |  Easy    |  https://leetcode.com/problems/power-of-three/      |
| #693. Binary Number with Alternating Bits           |  Easy    |  https://leetcode.com/problems/binary-number-with-alternating-bits/ |
| #137. Single Number II                              |  Medium  |  https://leetcode.com/problems/single-number-ii/                    |
| #338. Counting Bits                                 |  Easy    |  https://leetcode.com/problems/counting-bits/                       |
| Check if a number is a power of two                 |  ---     |  https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/  |
| Count total set bits in all numbers from 1 to N     |  ---     |  https://www.geeksforgeeks.org/count-total-set-bits-in-all-numbers-from-1-to-n/  |
| Turn off the rightmost set bit                      |  ---     |  https://www.geeksforgeeks.org/turn-off-the-rightmost-set-bit/   |
| Position of rightmost set bit                       |  ---     |  https://www.geeksforgeeks.org/position-of-rightmost-set-bit/    |


---

### **Counting Set Bits**
- Use `x &= (x - 1)` to remove the lowest set bit and keep counting until `x == 0`. This helps count the number of 1's (set bits) in the binary representation. Each `x &= (x - 1)` removes the lowest set bit, making it ideal for counting bits.

**Examples**:

| TITLE                                               | LEVEL    | SOURCE |  
| -----                                               | ----     | ----   |
| #191. Number of 1 Bits                              |  Easy    |  https://leetcode.com/problems/number-of-1-bits/     |
| #338. Counting Bits                                 |  Easy    |  https://leetcode.com/problems/counting-bits/        |
| #476. Number Complement                             |  Easy    |  https://leetcode.com/problems/number-complement/    |
| #89. Gray Code                                      |  Medium  |  https://leetcode.com/problems/gray-code/            |
| #67. Add Binary                                     |  Easy    |  https://leetcode.com/problems/add-binary/                       |
| #405. Convert a Number to Hexadecimal               |  Easy    |  https://leetcode.com/problems/convert-a-number-to-hexadecimal/  |
| Brian Kernighan's Algorithm                         |  ----    |  https://www.geeksforgeeks.org/count-set-bits-in-an-integer/ |
| Flip all bits of a number                           |  ----    |  https://www.geeksforgeeks.org/flip-bits-number/             |
| Swap all odd and even bits                          |  ----    |  https://www.geeksforgeeks.org/swap-all-odd-and-even-bits/   |
| Find parity of a number                             |  ----    |  https://www.geeksforgeeks.org/program-to-find-parity/       |

---

### 4. **Swapping Numbers Using XOR**

You can swap two numbers `x` and `y` without using a temporary variable with the following operations:
```
  1. `x = x ^ y`
  2. `y = x ^ y`
  3. `x = x ^ y`
```
XORing a number with itself results in 0, so swapping can be done in-place without using additional space.

**Examples**:

| TITLE                                               | LEVEL    | SOURCE |  
| -----                                               | ----     | ----   |
| #191. Number of 1 Bits                              |  Easy    |  https://leetcode.com/problems/number-of-1-bits/     |
| #136. Single Number                                 |  Easy    |  https://leetcode.com/problems/single-number/        |
| #137. Single Number II                              |  Medium  |  https://leetcode.com/problems/single-number-ii/     |
| #260. Single Number III                             |  Medium  |  https://leetcode.com/problems/single-number-iii/    |
| #645. Set Mismatch                                  |  Easy    |  https://leetcode.com/problems/set-mismatch/         |
| #268. Missing Number                                |  Easy    |  https://leetcode.com/problems/missing-number/       |
| Swap two numbers without a temporary variable       | ----     |  https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/ |
| Swap all odd and even bits                          | ----     | https://www.geeksforgeeks.org/swap-all-odd-and-even-bits/        |
| Find the only odd occurring element                 | ----     |  https://www.geeksforgeeks.org/find-the-element-that-appears-once/   |

---

### 5. **Reversing Bits**
Reversing the bits of a number involves extracting each bit and shifting it into its reverse position.

By shifting bits one at a time and using bitwise OR, you can reverse the order of bits in a number.


**Examples**:

| TITLE                                                     | LEVEL    | SOURCE |  
| -----                                                     | ----     | ----   |
| #190. Reverse Bits                                        |  Easy    |  https://leetcode.com/problems/reverse-bits/description/             |
| #405. Convert a Number to Hexadecimal                     |  Easy    |  https://leetcode.com/problems/convert-a-number-to-hexadecimal/      |
| #1290. Convert Binary Number in a Linked List to Integer  |  Easy    |  https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer/  |
| Reverse bits of a number                                  | ----     |  https://www.geeksforgeeks.org/reverse-actual-bits-given-number/     |
| Find whether a number is a palindrome in binary representation  | ----     |  https://www.geeksforgeeks.org/find-whether-a-given-number-is-a-palindrome/ |
| Reverse individual bits of a number                       | ----     |  https://www.geeksforgeeks.org/reverse-individual-bits-of-number/  |
| Reverse a linked list using bitwise operators             | ----     |  https://www.geeksforgeeks.org/reverse-a-linked-list/              |
| Convert Binary to Gray code                               | ----     |  https://www.geeksforgeeks.org/binary-to-gray-code-conversion/     |


Leet code similar problems: [https://leetcode.com/tag/bit-manipulation/](https://leetcode.com/tag/bit-manipulation/)