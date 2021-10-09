# 문제1 꿀벌

## 이전풀이

- https://github.com/hann3/zerobase-algorithm-001/blob/main/01-string/21-10-05-wonjongbin.md

## 작성 코드 
```javascript


function solution(work){
    // 출력해야 하는 작업과 순서를 담고 있는 리스트 
    let workList = ["Re", "Pt", "Cc", "Ea", "Tb", "Cm", "Ex"];
    let hMap = new Map();
    // "Cc Pt Pt Re Tb Re Cm Cm Re Pt Pt Re Ea Ea Pt Pt Pt Re Re Cb Cb Pt Pt Cb" 띄어쓰기로 구분 
    let arr = work.split(' ');

    for(let i=0; i<arr.length; i++){
        hMap.set(workList[i], 0);
    }
    for(let i=0; i<arr.length; i++){
        hMap.set(arr[i], (hMap.get(arr[i])||0) + 1);
    }
    // 필요한 작업만 출력 
    for(let i=0; i<workList.length; i++){
        // total = 전체 작업의 수 (arr)
        console.log(workList[i], " ", hMap.get(workList[i]), " ", (hMap.get(workList[i])/arr.length).toFixed(2));
    }
    console.log("Total ", arr.length);
}


```


# 문제2 같은 숫자는 싫어

## 이전풀이

- https://github.com/hann3/zerobase-algorithm-001/blob/main/02-array/21-10-06-ahnhyunseo.md

## 추가된 조건
- push로 별도의 공간에 추가하는 것이 아니라 arr 내에서 해결할 것 

## 작성 코드 
```javascript

function solution(arr)
{
    /* 0-9 */
    let prev = -1;
    return arr.filter(val=>{
        if (prev === val) return false;
        prev = val;
        return true;
    });
}


```



# 문제3 보석 쇼핑

## 이전풀이
- https://github.com/hann3/zerobase-algorithm-001/blob/main/03-two-pointers/21-10-07-hurjunhyuk.md

## 추가된 조건
- while을 사용하지 않고 for을 통해 해결할 것

## 작성 코드
```javascript
function solution(gems){
    const gemSet = new Set(gems);
    const sH =new Map(); 
    let answer = [];
    let left = 0; 
    // left는 유일 키를 보관하는 역할 
    let distance = Number.MAX_SAFE_INTEGER; 
    for(let right = 0; right < gems.length; right++){
        sH.set(gems[right], (sH.get(gems[right])||0)+1);
        // A,B,B,B,C,B,A 
        while(sH.get(gems[left]) > 1){
            sH.set(gems[left], (sH.get(gems[left])||0)-1);
            left++;
        }
        if(sH.size === gemSet.size){
            // 최소값을 저장 
            if (distance > right - left){
                distance = right - left;
                answer = [left + 1, right + 1];
            }
        }
    }
    return answer; 
}

```