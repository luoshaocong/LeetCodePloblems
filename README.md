#  LeetCode algorithm problems set



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

## Answer for problem 7

Write a program that outputs the string representation of numbers from 1 to n.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

Example:
```
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```
## Answer for problem 7

```
var fizzBuzz = function(n) {
 arr = []
 for(i = 1; i <=15; i++) {
    if(i % 3 === 0 && i % 5 === 0) {
         arr.push("fizzBuzz");

     }
     else if(i % 3 === 0) {
       arr.push("fizz");
    }
      else if(i % 5 === 0) {
       arr.push("buzz");
     }
     else {
         arr.push(i.toString());;
     }

 }
 return arr;


};

fizzBuzz(15)
```


## Question for problem 8
Consider all the leaves of a binary tree.  From left to right order, the values of those leaves form a leaf value sequence.



For example, in the given tree above, the leaf value sequence is (6, 7, 4, 9, 8).

Two binary trees are considered leaf-similar if their leaf value sequence is the same.

Return true if and only if the two given trees with head nodes root1 and root2 are leaf-similar.


## Answer for problem 8
```

var leafSimilar = function(root1, root2) {
    return helper(root1)===helper(root2);
};


var helper=function(root){
    var op=[];
    inorder(root,op);
    return op.join(",");
}

var inorder=function(root,op){
  if(!root.left && !root.right){
        op.push(root.val);
    }
    inorder(root.left,op);
    inorder(root.right,op);
}
```
## Question for problem 9
Given the root node of a binary search tree (BST) and a value. You need to find the node in the BST that the node's value equals the given value. Return the subtree rooted with that node. If such node doesn't exist, you should return NULL.

For example,
```
Given the tree:
        4
       / \
      2   7
     / \
    1   3

And the value to search: 2
```
You should return this subtree:
```

      2     
     / \   
    1   3
```
In the example above, if we want to search the value 5, since there is no node with value 5, we should return NULL.

Note that an empty tree is represented by NULL, therefore you would see the expected output (serialized tree format) as [], not null.


## Answer for problem 9
```

/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} val
 * @return {TreeNode}
 */


searchBST = function(root,val) {
  if(val < root) {
    return searchBST(root.left,val);
  }

  else if(val > root) {
    return searchBST(root.right,val);
  }

  else if(val === root){
    return root;
  }

    else return [];
}


```
