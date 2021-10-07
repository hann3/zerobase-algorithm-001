# 문제
[ 백준 14465번 ]

[소가 길을 건너간 이유 5](https://www.acmicpc.net/problem/14465)

# 문제요약
n개의 횡단보도가 존재하고 b개의 고장난 신호등이 있다 **최소 몇개를 고쳐서** 연속된 횡단보도(k개)를 만들 수 있을까?

# 접근방법
연속된 신호들의 개수를 지정해줬기대문에 초기값을 셋팅하고 left, right값을 증가시키며 고장난 신호들의 개수를 탐색한다

# 풀이
```js
const fs = require("fs");
const filePath = process.platform === 'linux' ? '/dev/stdin' : 'testcase/14465.txt';

let input = fs.readFileSync(filePath).toString().trim().split("\n");

// 횡단보도의 갯수(n)
const n = parseInt(input[0].split(" ")[0]);
// 연속한 신호등의 개수(k) 
const k = parseInt(input[0].split(" ")[1]);
// 고장난 신호등의 개수(b)
const b = parseInt(input[0].split(" ")[2]);

let result = n; // 최대값으로 초기화

let arr = new Array(n).fill(true); // 정상인 신호등은 true (모든 값을 true로 초기화)

for (let i = 1; i < b+1; i++){
    arr[input[i]-1] = false; // 고장난 신호등은 false
}

let cnt = 0; // 창안에 고장난 신호등의 개수를 나타낼 변수

// 초기 창을 셋팅
for (let i = 0; i < k-1; i++){
    if(arr[i] === false) cnt++;
}

let left = 0;

// 계산
for(let right = k-1; right < n; right++){
    if(arr[right] === false) cnt++;
    result = Math.min(result, cnt);
    if(arr[left] === false) cnt--;
    left++;
}

//결과
console.log(result);
```

## Tastcase
```
10 6 5
2
10
1
5
9
```

## 결과
```
1
```