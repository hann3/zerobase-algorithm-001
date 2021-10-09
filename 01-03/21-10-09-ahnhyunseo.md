# 문제1

[위장](https://programmers.co.kr/learn/courses/30/lessons/42578?language=javascript)

### 풀이 방법

```javascript

function solution(clothes) {
    var answer = 1, hash=new Map()
    for (let [_,i] of clothes) hash.set(i,(hash.get(i)||0)+1)
    // 옷들을 hash로 분류 (이름은 상관없기 때문에 개수만 세줌)
    for (let [_,v] of hash) answer*=(v+1)
    // hash 안의 각 (종류+1)을 전부 곱해줌
    // v+1 === 옷의 종류 + 안 입는 경우
    // 각각을 매치한 경우를 구함
    return answer-1
    // 모두 착용하지 않는 경우를 제외
}

```

---

# 문제2

[스킬트리](https://programmers.co.kr/learn/courses/30/lessons/49993?language=javascript)


```javascript

function solution(skill, skill_trees) {
    function sol(skill_tree){
        // skill_tree of slill_trees
        let _skill=skill.split('')
        // 배열로 담아 앞부터 하나씩 비교
        for(let sk of skill_tree){
            if(!skill.includes(sk) || sk===_skill.shift()) continue
            // js에서의 pop(0)===shift()
            // 현재 배우려는 skill이 선행 스킬이 아니거나 현재 배워야할 선행 스킬인 경우
            return false
            // 그 외, 현재 배우려는 skill이 선행 스킬이지만 순서에 맞지 않는 경우
        }
        return true
    }
    return skill_trees.filter(sol).length
    // true인 skill_tree만 return하여 개수를 셈
}

```

---
# 문제3

[소가 길을 건너간 이유 5](https://www.acmicpc.net/problem/14465)


- for
```javascript

function solution(N, K, B, n_list){
                let answer=K, cnt=0
                // answer의 최댓값: 모든 신호등을 고쳐야할 경우
                let arr=new Array(N).fill(0)
                for (let n of n_list) arr[n-1]=1
                // N개의 신호등에 대해 고장난 신호등은 1, 아닌 신호등은 0
                cnt=arr.slice(0,K-1).reduce((sum,v)=>{return sum =+ v})
                // K-1개까지의 값을 미리 구함
                for(let i=K-1;i<N;i++){
                    cnt+=arr[i]
                    // i===right
                    answer=answer>cnt ? cnt : answer
                    // 더 작은 값을 answer
                    cnt-=arr[i-K-1]
                    // i-k-1===left
                }
                // 1개 증가, 1개 감소로 일정하게 이동하여 변수 한 개만 사용
                return answer
            }
            console.log(solution(10, 6, 5, [2, 10, 1, 5, 9]))

```

- while
```javascript

function solution(N, K, B, n_list){
                let answer=K, cnt=0
                // answer의 최댓값: 모든 신호등을 고쳐야할 경우
                let arr=new Array(N).fill(0)
                for (let n of n_list) arr[n-1]=1
                // N개의 신호등에 대해 고장난 신호등은 1, 아닌 신호등은 0
                cnt=arr.slice(0,K-1).reduce((sum,v)=>{return sum =+ v})
                // K-1개까지의 값을 미리 구함
                let i=K-1
                // left, right 공통 변수
                while(i<N){
                    cnt+=arr[i]
                    // i===right
                    answer=answer>cnt ? cnt : answer
                    // 더 작은 값을 answer
                    cnt-=arr[i-K-1]
                    // i-k-1===left
                    i++
                }
                // 1개 증가, 1개 감소로 일정하게 이동하여 변수 한 개만 사용
                return answer
            }
            console.log(solution(10, 6, 5, [2, 10, 1, 5, 9]))

```
