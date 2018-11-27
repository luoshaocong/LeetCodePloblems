#  LeetCode algorithm problems set

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

## Problem 4

Given a non-empty array of integers, every element appears twice except for one. Find that single one.

## Answer for problem 4
```
var singleNumber = function(nums) {
  nums.sort();
  for(i = 0; i < nums.length; i++){
    if(i %2 === 0 && nums[i]!== nums[i+1]){
      return nums[i];
      
    }
  }
};
```
## Problem 5
Given an integer array, you need to find one continuous subarray that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too.

You need to find the shortest such subarray and output its length.

Example 1:
```
Input: [2, 6, 4, 8, 10, 9, 15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
```

## Answer for problem 5
```
var findUnsortedSubarray = function(nums) {
    cpy = nums.slice();
    nums.sort((a,b)=>{return a-b});
    start = 0;
    end = 0;   
    for(i = 0; i < nums.length; i++) {
        if(nums[i]!==cpy[i]) {
            start = i;
            break;
        }
    }
    for(j = nums.length; j>1 ; j--) {
      if(nums[j]!==cpy[j]) {
          end = j;
          break;
       }       

    }
    return j - i+1 ;
};
```

## Problem 6
Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

Example 1:
```
Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```
Example 2:
```
Input: "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
```
## Answer for problem 6
```
var countpalindromic = function(i,j,s) {
  count = 0;
  while(i >= 0 && j < s.length && s[i] === s[j]){
    count++;
    i--;
    j++;

  }
  return count;
};


var countSubstrings = function(s) {
  count = s.length;

  for(i = 0; i < s.length; i++){
    count += countpalindromic(i,i + 1,s) + countpalindromic(i, i+2, s);


  }

    return count;
};
countSubstrings("abba")




```
