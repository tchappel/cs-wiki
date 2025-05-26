# Arrays and Strings

## Sliding Window

A sliding window is a subarray defined by two pointers (indices):

- start (left bound) pointer
- end (right bound) pointer

**Idea**: The right bounds pointer moves through the array, while the left bounds pointer is adjusted based on some condition.

**Comlexity**: O(n) for both time and space, where n is the length of the array.

### Applications

- [find best valid subarray (e.g longest, max sum, etc.)](#best-valid-subarray)
- [find all valid subarrays](#number-of-subarrays)
- [find valid subarrays with a fixed window size](#fixed-window-size)

**Note**: sliding window technique itself finds the longest subarray that satisfies a condition, but it can be adapted to count all valid subarrays (read below).

### Find best valid subarray (e.g longest, max sum, etc.) {#best-valid-subarray}

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

### find all valid subarrays (Number of Subarrays) {#number-of-subarrays}

Find number of subarrays of nums whose product of all elements is strictly less than k.

**Trick**: sliding winow finds the longest subarray that satisfies the condition, but we need to count all valid subarrays. The number of valid subarrays ending at `right` is `right - left + 1`, because all subarrays starting from `left` to `right` are valid.

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

    ans += right - left + 1;
  }

  return ans;
};
```

### Fixed Window Size {#fixed-window-size}

When the size of the subarray is fixed, we can use a sliding window to find the best subarray of that size.

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
