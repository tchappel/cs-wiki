# Sliding Window

A sliding window is a subarray defined by two pointers (indices):

- start (left bound) pointer
- end (right bound) pointer

**Comlexity**: O(n) for both time and space, where n is the length of the array.

## Applications

- [find best valid subarray](#find-best-valid-subarray)
- [find all valid subarrays](#find-number-of-valid-subarrays)
- [find valid subarrays with a fixed window size](#fixed-window-size)

## Find best valid subarray

e.g longest, max sum, etc.

**Idea**: The right bounds pointer moves through the array, while the left bounds pointer is adjusted based on some condition.

Find the length of the longest subarray with elements sum <= k.

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var findLength = function (nums, k) {
  // curr is the current sum of the window
  let left = 0,
    curr = 0,
    ans = 0;
  for (let right = 0; right < nums.length; right++) {
    curr += nums[right];
    while (curr > k) {
      curr -= nums[left];
      left++;
    }

    ans = Math.max(ans, right - left + 1);
  }

  return ans;
};
```

## Find number of valid subarrays

Find number of subarrays of nums whose product of all elements is strictly less than k.

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var numSubarrayProductLessThanK = function (nums, k) {
  if (k <= 1) {
    return 0;
  }

  let ans = 0,
    left = 0,
    curr = 1;

  for (let right = 0; right < nums.length; right++) {
    curr *= nums[right];
    while (curr >= k) {
      curr /= nums[left];
      left++;
    }

    ans += right - left + 1; // all subarrays starting from `left` to `right` are valid.
  }

  return ans;
};
```

## Fixed Window Size {#fixed-window-size}

Find the maximum sum of any contiguous subarray of size k in the array nums.

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var findBestSubarray = function (nums, k) {
  let curr = 0;
  for (let i = 0; i < k; i++) {
    curr += nums[i];
  }

  let ans = curr;
  for (let i = k; i < nums.length; i++) {
    curr += nums[i] - nums[i - k];
    ans = Math.max(ans, curr);
  }

  return ans;
};
```
