# 1. 완주하지 못한 선수

## 문제 링크
[프로그래머스] [완주하지 못한 선수](https://programmers.co.kr/learn/courses/30/lessons/42576)

## 풀이
```js
const solve = (participant, completion) => {
    const hash = new Map();

    // 모든 참가자를 map으로 카운팅
    for (const p of participant){
        hash.set(p, (hash.get(p) || 0) + 1);
    }

    // 완주한 참가자들을 돌면서 참가자 map에 있는지 확인
    for (const c of completion){
        if(hash.has(c)){
            hash.set(c, hash.get(c) - 1);
            if(hash.get(c) === 0){
                hash.delete(c);
            }
        }
    }
    for(const key of hash) return key[0];
} 
```

# 2. Maximum Subarray

## 문제 링크
[leetCode] [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

## 풀이
```js
const solve = (nums) => {
    // 최소값
    let temp = -10000;
    let max = -10000;
    // 부분합
    for(const num of nums){
        temp = Math.max(temp+num, num);
        max = Math.max(max, temp);
    }
    return max;
}
```
# 3. Container With Most Water

## 문제 링크
[leetCode] [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

## 풀이
```js
const solve = (height) => {
    // 양 끝을 포인트로 셋팅
    let left = 0;
    let right = height.length-1;
    let max = 0;
    
    while(left < right){
        // 기존의 넓이를 더 큰값으로 갱신
        max = Math.max(Math.min(height[left], height[right]) * (right-left), max);
        // 최대값을 찾기때문에 높이가 더 낮은 쪽이 인덱스 변경
        height[left] < height[right] ? left++ : right--;
    }
    return max;
}
```