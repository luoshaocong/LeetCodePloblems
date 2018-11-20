#  LeetCode problems set

### all answer is written in javascript

## Problem 1

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Examples
```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

## Answer for problem 1

```
var maxSubArray = function(nums) {
  const hash = { 0: nums[0]}
  let max = nums[0];

  for (let i = 1; i < nums.length; i += 1) {
    hash[i] = Math.max(hash[i - 1] + nums[i], nums[i]);
    max = Math.max(hash[i], max);
  }

  return max;
};
```
