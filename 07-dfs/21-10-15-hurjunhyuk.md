# 문제

## 프로그래머스 - 타겟 넘버

reference: https://programmers.co.kr/learn/courses/30/lessons/43165

## 문제설명

n개의 음이 아닌 정수가 있습니다. 이 수를 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다.
예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.
```
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
```
사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

## 입출력

|numbers|target|return|
|----|----|----|
|[1, 1, 1, 1, 1]|3|5|

## 작성 코드

```js
function solution(nums, target) {
    let answer = 0;
    let n = nums.length;
    
    function DFS(L, sum) {
        // nums의 갯수만큼 깊이우선탐색을 하고
        if (L === n) {
            // -, +된 값의 합이 주어진 target과 일치할 경우
            // answer를 증가시켜준다.
            if (sum === target) {
                answer++;
            }
            // return이 없어도 동작의 변화는 없음
            return;
        } else {
            // 왼쪽 노드는 - 연산을 해주면서 깊이우선탐색 진행
            DFS(L + 1, sum - nums[L]);
            // 오른쪽 노드는 + 연산을 해주면서 깊이우선탐색을 진행
            DFS(L + 1, sum - nums[L]);+ 연산을 해주면서 
        }
    }
    // 레벨0, 합계0으로부터 깊이우선탐색 시작
    DFS(0, 0);
    return answer;
}
```
