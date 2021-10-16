# 문제
[Combination Sum](https://leetcode.com/problems/combination-sum/)

# 접근방향
- dfs를 이용하고, 중복이 가능하니가 for문의 i를 0부터 시작해보자!
- 8이 될때, [2, 3, 3], [3, 2, 3], [3, 3, 2]는 하나로 취급되어야함!

# 풀이

## 첫번재 문재해결
```js
const solve = (candidates, target) => {
    // 중복을 피하기 위해서 Set을 사용
    const answer = new Set();
    let sum = 0;
    const temp = [];

    const DFS = (sum) => {
        if(sum > target) return;
        if(sum === target){
            // set에 넣을때 중복을 피하기 위해서 temp를 복사하고, 정렬한 후에 합친다
            // - 는 한자리 수, 두자리 수 ... 를 구분하기 위해서
            answer.add(temp.slice().sort((a, b) => a - b).join("-"));
        }
        else{
            for(const c of candidates){
                temp.push(c);
                DFS(sum + c);
                temp.pop();
            }
        }
    }
    DFS(sum);
    // ([2-3-3, 3-2-3, 3-3-2]) 형태이므로 배열로 변환 후 나머지 작업처리
    return [...answer].map(item => item.split("-").map(item2 => +item2));
}
console.log(solve([2,3,5], 8))
```


## 두번째 문제해결
```js
const solve = (candidates, target) => {
    const answer = [];
    let sum = 0;
    const temp = [];
    const len = candidates.length;

    const DFS = (s, sum) => {
        if(sum > target) return;
        if(sum === target){
            answer.push([...temp]);
        }
        else{
            // 생각해보니 앞에서 나온 수를 다시 할필요가 없다 (이미 앞에서 같은 수의 조합을 결과에 추가했기 때문!!)
            for(let i = s; i < len; i++){
                temp.push(candidates[i]);
                DFS(i, sum + candidates[i]);
                temp.pop();
            }
        }
    }
    DFS(0, sum);
    return answer;
}
console.log(solve([2,3,5], 8))
```

# 입력값
```
[2,3,5],8
```
# 출력
```
[[2,2,2,2],[2,3,3],[3,5]]
```