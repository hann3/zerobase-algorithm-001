# [프로그래머스 - 해시]위장

reference: https://programmers.co.kr/learn/courses/30/lessons/42578

```js
function solution(clothes) {
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
