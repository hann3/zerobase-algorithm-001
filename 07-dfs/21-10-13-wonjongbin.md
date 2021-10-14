# 문제
[타겟넘버](https://programmers.co.kr/learn/courses/30/lessons/43165)

# 접근방향
더하고 빼고 두가지 경우!

# 풀이
```js
function solution(numbers, target) {
    var answer = 0;
    let temp = 0;

    const dfs = (L) => {
        // L이 numbers의 길이만큼 = 다 사용
        if(L === numbers.length){
            // target과 같은 경우 answer 더해주기
            if(temp === target) {
                answer++;
            }
            return;
        // 더하고 빼고 두가지 경우
        }else{
            // 더해주는 경우
            temp += numbers[L];
            dfs(L+1);
            // 빼주는 경우
            temp -= (2 * numbers[L]);
            dfs(L+1);
            // 다시 원래대로
            temp += numbers[L];
        }
    }
    dfs(0);
    return answer;
}
```

# 입력값
```
[[1, 1, 1, 1, 1], 3]
```
# 출력
```
5
```