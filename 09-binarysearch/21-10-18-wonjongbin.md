# 문제
[입국심사](https://programmers.co.kr/learn/courses/30/lessons/43238)

# 접근방향
<u>주어진 시간안에 심사대에서 인원을 심사할 수 있는가?</u> 에서 시작!
- 각 심사대에서 주어진 시간동안 몇명을 심사할 수 있는지의 총합으로 비교

# 풀이
```js
function solution(n, times) {
    var answer = 0;
    
    // 최소시간과 가장 오래 걸리는 시간을 계산
    let left = 1;
    let right = Math.max(...times)*n;

    while(left <= right){
        let mid = parseInt((left + right) / 2);
    
        // 모든 심사대에서 주어진 시간(mid)동안 몇명의 사람을 심사할 수 있는지, 총합을 게산
        let sum = times.reduce((prev, curr) => {
            return prev + parseInt(mid/curr);
        }, 0);
        
        // 만약 심사할 수 있는 인원이 더 많으면 시간을 줄여주고, 인원을 모두 심사할 수 없으면 시간을 늘려준다
        if(n <= sum){
            right = mid - 1;
            // 최소시간을 구하므로 right를 줄일때 answer를 업데이트한다
            answer = mid;
        }else{
            left = mid + 1;
        }
    }
    return answer;
}
```

# 입력값
```
6, [7, 10]
```

# 출력
```
28
```