# 문제1

[Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

### 문제 설명
Given an array of positive integers nums and a positive integer target, return the minimal length of a contiguous subarray [numsl, numsl+1, ..., numsr-1, numsr] of which the sum is greater than or equal to target. If there is no such subarray, return 0 instead.
- 부분 문자열의 합이 target보다 크거나 같은 경우 중, 부분 문자열의 길이가 가장 짧을 때의 길이 구하기

### 제한사항
- 1 <= target <= 109
- 1 <= nums.length <= 105
- 1 <= nums[i] <= 105

### INPUT
nums = [2,3,1,2,4,3]
target = 7


### OUTPUT
2

```javascript

function(target, nums) {
    let sum=0, left=0, answer=Number.MAX_SAFE_INTEGER
    for(let right=0;right<nums.length;right++){
        sum+=nums[right]
        // sum에 값 추가
        while(sum>=target){
            // 기본적으로 부분 문자열의 길이가 가장 짧을 때를 찾아야하므로 앞부분을 빼주는 방식으로 문자열 크기를 줄여나감
            answer=Math.min(answer,right-left+1)
            // 조건이 크거나 같을 때이므로, 클 때도 길이 검사를 해줌
            sum-=nums[left++]
        }
    }
    if(answer===Number.MAX_SAFE_INTEGER) return 0
    // 만약 전체의 합이 target보다 작을 경우 0리턴
    return answer
}

```
