[타겟 넘버](https://programmers.co.kr/learn/courses/30/lessons/43165?language=javascript)

### 문제 설명
numbers로 들어오는 숫자들을 더하거나 빼서 나온 값이 target이 되는 개수를 반환

### 제한 사항
- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
- 각 숫자는 1 이상 50 이하인 자연수입니다.
- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.

### INPUT
numbers
[1,1,1,1,1]

target
3

### OUTPUT
5

```javascript
function solution(numbers, target) {
    let answer = 0
    let len=numbers.length
    function DFS(L, sum){
        if(L===len){
            if(sum===target) answer++
	// 전부 순회하고, 총 값이 target일 경우에만 answer 증가
            return
	// 종료
        }
        else{
            DFS(L+1, sum-numbers[L])
	// 값 빼기
            DFS(L+1, sum+numbers[L])
	// 값 더하기
        }   
    }
    DFS(0,0)
    return answer
}
```