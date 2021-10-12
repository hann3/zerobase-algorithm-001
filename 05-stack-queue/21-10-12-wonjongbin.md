# 문제
[기능 개발](https://programmers.co.kr/learn/courses/30/lessons/42586?language=javascript)

# 접근방향
progresses 요소 하나 하나를 100%가 되었을때 앞에서부터 차례로 지워주며 카운팅

# 풀이
```js
function solution(progresses, speeds) {
    var answer = [];
    // 작업이 없을때까지
    while(progresses.length > 0){
        // 모든 작업내용을 돌면서 진행률 증가
        for(let i = 0; i < progresses.length; i++){
            // 각각 진행률 증가시킴
            progresses[i] = progresses[i] + speeds[i];
            // 만약 제일 앞에 있는 작업이 100%를 넘게되면
        }
        if(progresses[0] >= 100){
            let cnt = 0; 
            // 뒤로 있는 100% 이상의 작업을 모두 shift하면서 counting
            while(progresses[0] >= 100){
                progresses.shift();
                speeds.shift();
                cnt++;
            }
            // 결과를 저장하는 배열에 push
            answer.push(cnt);
        }
    }
    return answer;
}

console.log(solution([93, 30, 55], [1, 30, 5]));
console.log(solution([95, 90, 99, 99, 80, 99], [1, 1, 1, 1, 1, 1]));
console.log(solution([100, 99, 99, 99, 99, 99], [1, 1, 1, 1, 1, 1]));
```

# 입력값
```
[93, 30, 55], [1, 30, 5]
[95, 90, 99, 99, 80, 99], [1, 1, 1, 1, 1, 1]
[100, 99, 99, 99, 99, 99], [1, 1, 1, 1, 1, 1]
```
# 출력
```
[ 2, 1 ]
[ 1, 3, 2 ]
[ 6 ]
```