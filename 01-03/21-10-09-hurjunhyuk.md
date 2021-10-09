## 1. [프로그래머스] 전화번호 목록

### 문제링크

- https://programmers.co.kr/learn/courses/30/lessons/42577

### 이전풀이

- 한나님: https://github.com/hann3/zerobase-algorithm-001/blob/main/01-string/21-10-05-choihanna.md

### 풀이조건

- 해시 이용해서

### 소스코드

```js
function solution(nums) {
  let sH = new Map();
  let min_length = Number.MAX_SAFE_INTEGER;
  let max_length = Number.MIN_SAFE_INTEGER;

  for (let i = 0; i < nums.length; i++) {
    if (sH.has(nums[i])) {
      return false;
    }
    sH.set(nums[i], (sH.get(nums[i]) || 0) + 1);
    min_length = Math.min(min_length, nums[i].length);
    max_length = Math.max(max_length, nums[i].length);
  }
  for (let split_len = min_length; split_len < max_length; split_len++) {
    for (let i = 0; i < nums.length; i++) {
      if (nums[i].length < split_len) {
        continue;
      }
      tmp = nums[i].substring(0, split_len + 1);
      if (sH.has(tmp)) {
        return false;
      }
    }
  }
  return true;
}

input = [
  ["119", "97674223", "1195524421"],
  ["123", "456", "789"],
  ["12", "123", "1235", "567", "88"]
];
output = [false, true, false];

for (let i = 0; i < input.length; i++) {
  console.log(output[i], solution(input[i]));
}
```

## 2. [백준] OX퀴즈(8958번)

### 문제링크

- https://www.acmicpc.net/problem/8958

### 이전풀이

- 종빈님: https://github.com/hann3/zerobase-algorithm-001/blob/main/02-array/21-10-06-wonjongbin.md

### 풀이조건

- 배열에 저장하는 방법 말고 for문 안에서 해결해보기

### 소스코드

```js
function solution(OX_result) {
  let answer = 0;
  let score = 0;

  for (let i = 0; i < OX_result.length; i++) {
    if (OX_result[i] === "O") {
      score++;
    } else {
      score = 0;
    }
    answer += score;
  }
  return answer;
}

input = [
  "OOXXOXXOOO",
  "OOXXOOXXOO",
  "OXOXOXOXOXOXOX",
  "OOOOOOOOOO",
  "OOOOXOOOOXOOOOX"
];
output = [10, 9, 7, 55, 30];

for (let i = 0; i < input.length; i++) {
  console.log(output[i], solution(input[i]));
}
```

## 3. [Minimum Size Subarray Sum]

### 문제링크

- https://leetcode.com/problems/minimum-size-subarray-sum

### 이전풀이

- 현서님: https://github.com/hann3/zerobase-algorithm-001/blob/main/03-two-pointers/21-10-07-ahnhyunseo.md

### 풀이조건

- 없음

### 소스코드

```js
function solution(nums, target) {
  let answer = Number.MAX_SAFE_INTEGER;
  let left = 0;
  let sum = 0;

  for (let right = 0; right < nums.length; right++) {
    sum += nums[right];
    while (sum > target) {
      sum -= nums[left++];
    }
    if (sum === target) {
      answer = Math.min(answer, right - left + 1);
    }
  }
  if (answer === Number.MAX_SAFE_INTEGER) return 0;
  return answer;
}

input1 = [
  [2, 3, 1, 2, 4, 3],
  [1, 4, 4],
  [1, 1, 1, 1, 1, 1, 1, 1]
];
input2 = [7, 4, 11];
output = [2, 1, 0];

for (let i = 0; i < input1.length; i++) {
  console.log(output[i], solution(input1[i], input2[i]));
}
```
