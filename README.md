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


## Problem 2
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Examples

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
## Answer for problem 2


Time complexity:O(n).
Space complexity:O(n).
```


function twoSum(nums, target) {
  var twoSum = [];
  nums.forEach((num, i) =>{
    var diff = target - num;
    var j = nums.indexOf(diff)
    if (j > -1 && j !== i) {
       twoSum[0] = i;
       twoSum[1] = j;
       return true;
    }
  })
  return twoSum;
}

```


## Problem 3


You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

Example 1:
```

Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps

```
Example 2:
```

Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```
## Answer for problem 3


```

var climbStairs = function(n, memo = {}) {
    if(n <= 1) return 1;

    memo[n] = memo[n] || climbStairs(n-1, memo) + climbStairs(n-2, memo);

    return memo[n];
};

```
