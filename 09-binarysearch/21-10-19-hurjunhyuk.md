# 문제

## 프로그래머스 - 입국심사

reference: https://programmers.co.kr/learn/courses/30/lessons/43238?language=javascript

## 문제설명

n명이 입국심사를 위해 줄을 서서 기다리고 있습니다. 각 입국심사대에 있는 심사관마다 심사하는데 걸리는 시간은 다릅니다.

처음에 모든 심사대는 비어있습니다. 한 심사대에서는 동시에 한 명만 심사를 할 수 있습니다. 가장 앞에 서 있는 사람은 비어 있는 심사대로 가서 심사를 받을 수 있습니다. 하지만 더 빨리 끝나는 심사대가 있으면 기다렸다가 그곳으로 가서 심사를 받을 수도 있습니다.

모든 사람이 심사를 받는데 걸리는 시간을 최소로 하고 싶습니다.

입국심사를 기다리는 사람 수 n, 각 심사관이 한 명을 심사하는데 걸리는 시간이 담긴 배열 times가 매개변수로 주어질 때, 모든 사람이 심사를 받는데 걸리는 시간의 최솟값을 return 하도록 solution 함수를 작성해주세요.

## 제한사항

입국심사를 기다리는 사람은 1명 이상 1,000,000,000명 이하입니다.
각 심사관이 한 명을 심사하는데 걸리는 시간은 1분 이상 1,000,000,000분 이하입니다.
심사관은 1명 이상 100,000명 이하입니다.

## 입출력

| n   | times   | return |
| --- | ------- | ------ |
| 6   | [7, 10] | 28     |

## 작성 코드

```js
function solution(n, times) {
    let answer;
    // 최소 시간 1분
    let left = 1;
    // 최대 시간 === 가장 오래걸리는 사람이 모두 처리한 시간
    let right = Math.max(...times) * n;
    // 최소시간이 최대시간보다 같거나 작을 때까지 반복
    while (left <= right) {
        // 이분탐색을 위한 중간값 구해주고
        let mid = parseInt((left + right) / 2);
        // mid 시간 기준으로 입국가능한 사람 숫자 구하기
        let people = 0;
        for (let x of times) {
            people += parseInt(mid / x);
        }
        // left, right값 조정
        if (n <= people) right = mid - 1;
        else left = mid + 1;
    }
    // 최소시간이므로 left값 리턴
    return left;
}
```
