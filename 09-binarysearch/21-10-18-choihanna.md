
# 문제

[입국 심사](https://programmers.co.kr/learn/courses/30/lessons/43238) 

## 문제 설명 

n명이 입국심사를 위해 줄을 서서 기다리고 있습니다. 각 입국심사대에 있는 심사관마다 심사하는데 걸리는 시간은 다릅니다.

처음에 모든 심사대는 비어있습니다. 한 심사대에서는 동시에 한 명만 심사를 할 수 있습니다. 가장 앞에 서 있는 사람은 비어 있는 심사대로 가서 심사를 받을 수 있습니다. 하지만 더 빨리 끝나는 심사대가 있으면 기다렸다가 그곳으로 가서 심사를 받을 수도 있습니다.

모든 사람이 심사를 받는데 걸리는 시간을 최소로 하고 싶습니다.

입국심사를 기다리는 사람 수 n, 각 심사관이 한 명을 심사하는데 걸리는 시간이 담긴 배열 times가 매개변수로 주어질 때, 모든 사람이 심사를 받는데 걸리는 시간의 최솟값을 return 하도록 solution 함수를 작성해주세요.

## 제한 사항  
  
* 입국심사를 기다리는 사람은 1명 이상 1,000,000,000명 이하입니다.
* 각 심사관이 한 명을 심사하는데 걸리는 시간은 1분 이상 1,000,000,000분 이하입니다.
* 심사관은 1명 이상 100,000명 이하입니다.

## 입출력 예시
  
    
|n|times|return|
|------|------|------|
|6|[[7, 10]|28|  


## 접근 방식
> 시간이 주어졌을 때 몇 명의 입국 심사를 처리할 수 있는가? 
> n과 같거나 n보다 많은 인원을 수용할 수 있을 경우 더 최소 시간을 찾는다 
  
  

# 구현 코드  

```javascript  

function solution(n, times){
    let answer = 0;
    let start = 0;
    let end = Math.max(...times)*n;
    // 최대 시간 = 가장 많은 시간이 소모되는 심사관 * 기다리는 사람 
    while(start <= end){
        let mid = parseInt((start+end)/2);
        if(countPassenger(mid) >= n){
            // n보다 높거나 같을 경우 현재 값을 저장한 뒤 계속해 최소 시간을 찾는다
            // answer에 최종적으로 저장되는 값은 최적의 값 
            answer = mid;
            end = mid - 1;
        }
        else start = mid + 1;
    }
    function countPassenger(time){
        let tmp = 0;
        for(let i=0; i<times.length; i++){
            tmp += parseInt(time / times[i]);
        }
        return tmp;
    }
    return answer;
}  

```