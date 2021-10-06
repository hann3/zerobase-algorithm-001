## leetcode 53. Maximum Subarray

reference: https://leetcode.com/problems/maximum-subarray/

Given an integer array nums, find the contiguous subarray (containing at least one number)
which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

Example 1:
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```
Example 2:
```
Input: nums = [1]
Output: 1
```
Example 3:
```
Input: nums = [5,4,-1,7,8]
Output: 23
```
```js
const maxSubArray = function (nums) {
    /* 반복문 */
    // for (let i = 1; i < nums.length; i++) {
    //     if (nums[i - 1] > 0)
    //         nums[i] += nums[i - 1];
    // }
    /* forEach */
    nums.forEach((val, i) => {
        if (nums[i - 1] > 0)
            nums[i] = val + nums[i - 1];
    })
    /* 최대값 리턴 */
    return Math.max(...nums);
};
```
