# 문제 [39. Combination Sum](https://leetcode.com/problems/combination-sum/)

### 문제 설명
- 주어진 배열 내에서 중복을 허용하여 생성한 조합이 taget이 될 때 출력

### INPUT
- candidates
[2,3,6,7]
[2,3,5]
- target
7
8

### OUTPUT
[[2,2,3],[7]]
[[2,2,2,2],[2,3,3],[3,5]]

```javascript

var combinationSum = function(candidates, target) {
    let answer = []
    let tmp=[]
    let n=candidates.length
    function DFS(sum, s) {
        if (sum === target) answer.push(tmp.slice())
            // 합이 target일 때 배열 추가
        else if(sum>target) return
            // 합이 target을 넘을 때 return
        else {
            for (let i = s; i < n; i++) {
                // 중복조합이기 때문에, 지나간 숫자는 고려하지 않으면서, 현재 숫자는 포함 가능
                tmp.push(candidates[i])
                DFS(sum+candidates[i],i)
                // 중복 허용이기 때문에 i+1(X), i(O) 
                tmp.pop()
            }
        }
    }
    DFS(0,0)
    return answer
}

```