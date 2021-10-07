## leetcode 53. Maximum Subarray

reference: https://leetcode.com/problems/maximum-subarray/

### 문제설명
Given an integer array nums, find the contiguous subarray (containing at least one number)
which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

### 접근방법
배열 내부의 연속되는 부분배열의 합이 최대가 되는 것을 고르는 문제
리턴값이 부분배열이 아니라 `부분배열의 합`

1. 0번 인덱스부터 마지막 인덱스까지 loop문을 통해 각 인덱스가 가질 수 있는 최대값을 구함
2. 배열 중 최대값을 리턴

### 입출력
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
### 작성코드
```js
function my_answer(nums) {
  for (let i = 1; i < nums.length; i++) {
    /* 해당 인덱스가 가질 수 있는 최대값을 구하려면 */
    /* 이전 인덱스에 있는 값이 양수여야 함 */
    if (nums[i - 1] > 0)
      nums[i] += nums[i - 1];
  }
  /* 최대값 리턴 */
  return Math.max(...nums);
};
```

### 테스트코드
```js
input = [
  [-2,1,-3,4,-1,2,1,-5,4],
  [1],
  [5,4,-1,7,8]
]

output = [
  6,
  1,
  23
]

for (let i = 0; i < input.length; i++) {
  console.log("input:", input[i], "got:", my_answer(input[i]), "want:", output[i]);
}
```
