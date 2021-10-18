# [입국심사]()

### 문제 설명
입국심사를 기다리는 사람 수 n, 각 심사관이 한 명을 심사하는데 걸리는 시간이 담긴 배열 times가 매개변수로 주어질 때,
모든 사람이 심사를 받는데 걸리는 시간의 최솟값을 return 하도록 solution 함수를 작성해주세요.

### 제한 사항
- 입국심사를 기다리는 사람은 1명 이상 1,000,000,000명 이하입니다.
- 각 심사관이 한 명을 심사하는데 걸리는 시간은 1분 이상 1,000,000,000분 이하입니다.
- 심사관은 1명 이상 100,000명 이하입니다.

### INPUT
n: 6
times: [7, 10]

### OUTPUT
28

```javascript

function solution(n, times) {
    let answer = 0
    function waiting(left, right){
        if(left>=right) return
        let middle=parseInt((left+right)/2)
        let sum=0
        
        for(let time of times) sum+=Math.floor(middle/time)
        // 정해진 시간(middle)동안 각 입국심사자들이 몇명을 맡을 수 있는 지 계산
        
        if(n<=sum){
            // n보다 많은 인원을 맡을 수 있다면, 시간을 줄여서 검색
            answer=middle
            waiting(left, middle)
        }
        else waiting(middle+1, right)
        // n보다 적다면, 시간을 늘려서 검색
    }
    waiting(0, Math.min(...times)*n)
    // 최대는 가장 적게 걸리는 사람이 모든 인원을 맡을 때로
    return answer
}

```