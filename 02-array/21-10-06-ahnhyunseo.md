# 문제1

[음양 더하기](https://programmers.co.kr/learn/courses/30/lessons/76501)

### 문제 설명
어떤 정수들이 있습니다.
이 정수들의 절댓값을 차례대로 담은 정수 배열 absolutes와 이 정수들의 부호를 차례대로 담은 불리언 배열 signs가 매개변수로 주어집니다.
실제 정수들의 합을 구하여 return 하도록 solution 함수를 완성해주세요.

### 제한사항
- absolutes의 길이는 1 이상 1,000 이하입니다.
	- absolutes의 모든 수는 각각 1 이상 1,000 이하입니다.
- signs의 길이는 absolutes의 길이와 같습니다.
	- signs[i] 가 참이면 absolutes[i] 의 실제 정수가 양수임을, 그렇지 않으면 음수임을 의미합니다.

### INPUT
absolutes	signs
[4,7,12]	[true, false, true]
[1,2,3]	[false, false, true]


### OUTPUT
9
0

```javascript

function solution(absolutes, signs) {
    let answer=0
    for(let i=0; i<signs.length; i++){
        // 두 배열의 길이가 같으므로 배열 하나의 길이를 기준으로 반복함
        if(signs[i]){
            // signs가 true일 경우 (양수인 경우)
            answer += absolutes[i]
            // 그대로 더해줌
        } else{
            // signs가 false일 경우 (음수인 경우)
            answer -= absolutes[i]
            // 전체에서 빼줌 (음수를 더함)
        } 
    }
    return answer
}

```


---
# 문제2

[같은 숫자는 싫어](https://programmers.co.kr/learn/courses/30/lessons/12906)

### 문제 설명
- 배열 arr의 각 원소는 숫자 0부터 9까지로 이루어져 있음
- 이때, 배열 arr에서 연속적으로 나타나는 숫자는 하나만 남기고 전부 제거
- 단, 배열 arr 원소들의 순서를 유지하며 반환

### 제한사항
- 배열 arr의 크기 : 1,000,000 이하의 자연수
- 배열 arr의 원소의 크기 : 0보다 크거나 같고 9보다 작거나 같은 정수

### INPUT
arr
[1,1,3,3,0,1,1]
[4,4,4,3,3]	

### OUTPUT
[1,3,0,1]
[4,3]

```javascript

function solution(arr){
    var answer = []
    arr.push('')
    // 마지막 문자 비교 위해 배열 마지막에 빈 문자 추가
    for(let i=0;i<arr.length-1;i++){
        // i는 원래있던 문자까지 돌기 위해 `문자열의 길이-1`보다 작을 때까지만 반복
        // arr[arr.length-1]은 ''
        if(arr[i]!==arr[i+1]){
            // 현재 문자와 다음 문자를 비교
            // 달라진다면 현재 문자를 answer에 추가
            answer.push(arr[i])
        }
    }
    return answer
}

```


