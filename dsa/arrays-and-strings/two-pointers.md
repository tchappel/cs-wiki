# Two Pointers

Use **two integer indices** ( **i** and **j**, or **left** and **right** ) to traverse an iterables (arrays or strings), each represent an index of the array or string, and Moving them according to problem-specific logic.

**Complexity**: O(n) time and O(1) space.

## Converging Pointers

**Idea**:

- Start one pointer at the first index 0 and the other pointer at the last index input.length - 1.
- Use a while loop until the pointers are equal to each other.
- At each iteration of the loop, move the pointers towards each other. This means either increment the pointer that started at the first index, decrement the pointer that started at the last index, or both. Deciding which pointers to move will depend on the problem we are trying to solve

**Blueprint**:

```text
function fn(arr):
    left = 0
    right = arr.length - 1

    while left < right:
        Do some logic here depending on the problem
        Do some more logic here to decide on one of the following:
            1. left++
            2. right--
            3. Both left++ and right--
```

**Example**: Check if a string is a palindrome.

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var checkIfPalindrome = function (s) {
  let left = 0;
  let right = s.length - 1;

  while (left < right) {
    if (s[left] != s[right]) {
      return false;
    }

    left++;
    right--;
  }

  return true;
};
```

**Example**: Two Sum II - Input Array Is Sorted, find if two numbers in a sorted array add up to a target value.

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {boolean}
 */
var checkForTarget = function (nums, target) {
  let left = 0;
  let right = nums.length - 1;

  while (left < right) {
    // curr is the current sum
    let curr = nums[left] + nums[right];
    if (curr == target) {
      return true;
    }

    if (curr > target) {
      right--;
    } else {
      left++;
    }
  }

  return false;
};
```

## Parallel Pointers

These involve problems that require traversing two iterables (arrays or strings) at the same time, using two pointers that move independently of each other.

**Idea**:

- Start both pointers at the first index 0.
- Use a while loop until one of the pointers reaches the end of the input.
- At each iteration of the loop, move one or both pointers according to the problem we are trying to solve.

**Blueprint**:

```text
function fn(arr1, arr2):
    i = j = 0
    while i < arr1.length AND j < arr2.length:
        Do some logic here depending on the problem
        Do some more logic here to decide on one of the following:
            1. i++
            2. j++
            3. Both i++ and j++

    // Step 4: make sure both iterables are exhausted
    // Note that only one of these loops would run
    while i < arr1.length:
        Do some logic here depending on the problem
        i++

    while j < arr2.length:
        Do some logic here depending on the problem
        j++
```

**Example**: Merge Two Sorted Array into one sorted array.

```javascript
/**
 * @param {number[]} arr1
 * @param {number[]} arr2
 * @return {number[]}
 */
var combine = function (arr1, arr2) {
  let ans = [];
  let i = 0,
    j = 0;

  while (i < arr1.length && j < arr2.length) {
    if (arr1[i] < arr2[j]) {
      ans.push(arr1[i]);
      i++;
    } else {
      ans.push(arr2[j]);
      j++;
    }
  }

  while (i < arr1.length) {
    ans.push(arr1[i]);
    i++;
  }

  while (j < arr2.length) {
    ans.push(arr2[j]);
    j++;
  }

  return ans;
};
```

**Example** check if string (s) is a subsequence of another string (t).

```javascript
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isSubsequence = function (s, t) {
  let i = 0,
    j = 0;
  while (i < s.length && j < t.length) {
    if (s[i] == t[j]) {
      i++;
    }

    j++;
  }

  return i == s.length;
};
```
