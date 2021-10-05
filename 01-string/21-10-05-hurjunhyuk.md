# [프로그래머스 - 해시]

## 위장

reference: https://programmers.co.kr/learn/courses/30/lessons/42578

```js
function solution(clothes) {
    'use strict'
    let answer = 1;
    let sH = new Map();
    for (let [val, key] of clothes) {
        sH.set(key, (sH.get(key) || 0) + 1);
    }
    for (let [key, val] of sH) {
        answer *= (val + 1);
    }
    return answer - 1;
}
```

## 완주하지 못한 선수

reference: https://programmers.co.kr/learn/courses/30/lessons/42576

```js
function solution(participant, completion) {
    'use strict'
    let answer = "";
    let sH = new Map();

    for (let x of participant) {
        sH.set(x, (sH.get(x) || 0) + 1);
    }
    for (let x of completion) {
        sH.set(x, (sH.get(x) || 0) - 1);
    }
    for (let x of participant) {
        if (1 === sH.get(x)) {
            answer = x;
            break;
        }
    }
    return answer;
}
```
