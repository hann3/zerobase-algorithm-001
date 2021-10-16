# 문제

[Combination Sum](https://leetcode.com/problems/combination-sum/) 

## 문제설명

Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.

The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is guaranteed that the number of unique combinations that sum up to target is less than 150 combinations for the given input.


## 입출력 예시


|candidates|target|output|
|------|------|------|
|[2, 3, 6, 7]|7|[[2, 2, 3], [7]]|
|[2, 3, 5]|8|[[2, 2, 2, 2],[2, 3, 3], [3,5]]|
|[2]|1|[]|
|[1]|1|[[1]]|
|[1]|2|[[1, 1]]|


# 작성 코드 

```javascript


var combinationSum = function(candidates, target) {
    let answer = [];
    let tmp = [];
    let len = candidates.length;
    candidates.sort((a, b)=>a-b);
    function searchCombi(L, sum){
        // sum이 커졌을 때 종료 
        if(sum > target) return ; 
        if(sum === target){
            answer.push(tmp.slice());
        } 
        else {
                for(let i=L; i < len; i++){
                    tmp.push(candidates[i]);
                    // 이전 원소로는 만들 수 없음 
                    searchCombi(i, sum + candidates[i]);
                    tmp.pop(); 
            }
        }
        
    }
    searchCombi(0, 0);
    return answer;
};


```