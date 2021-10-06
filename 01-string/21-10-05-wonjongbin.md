# 문제
[ 백준 9733번 ]

[꿀벌문제](https://www.acmicpc.net/problem/9733)



# 풀이
```js
// 꿀벌의 일목록(7가지)
// 휴식(Re), 순찰(Pt), 방청소(Cc), 꽃가루 먹기(Ea), 새끼 돌보기(Tb), 벌집 짓기와 관리(Cm), 외부 활동(Ex)

const fs = require("fs");
const filePath = process.platform === 'linux' ? '/dev/stdin' : 'testcase/9733.txt';

// 공백 또는 줄바꿈으로 문자열이 입력
let input = fs.readFileSync(filePath).toString().trim().split("\n").map((item) => item.trim().split(" "));;

// 한 배열에 모든 값 집어넣기
let beaWorked = [].concat(...input);

// 일목록
let workList = ["Re", "Pt", "Cc", "Ea", "Tb", "Cm", "Ex"];
let work = new Map();

// 주어진 작업을 map으로, 0으로 초기화
for (const workThing of workList){
    work.set(workThing, 0);
}

// set, get, has를 이용해서 작업이 존재할때, 존재하지 않을때, total을 구해준다
for (const worked of beaWorked){
    work.set("Total", (work.get("Total") || 0) + 1)
    if(work.has(worked)){
        work.set(worked, work.get(worked) + 1)
    }
}

// 출력: map을 돌면서 처리
for (const key of work){
    console.log(`${key[0]} ${key[1]} ${(work.get(key[0])/work.get("Total")).toFixed(2)}`)
}
```

## 사용한 js

- `toString()`: 문자열로 변환
- `trim()`: 양쪽 공백제거
- `map()`: 배열에서 각 항목에 대한 작업수행
- `concat()`: 인자로 들어온 배열이나 값들을 합침
- `toFixed()`: 인자로 들어온 숫자까지 반올림해서 문자열로 리턴
- 삼항연산자: `(조건) ? (조건이 참일때) : (조건이 거짓일때)`


## Tastcase

```
Cc Pt Pt Re Tb Re Cm Cm Re Pt Pt Re Ea Ea Pt Pt
Pt Re Re Cb Cb 
Pt Pt Cb
```

## 결과
```
Re 6 0.25
Pt 9 0.38
Cc 1 0.04
Ea 2 0.08
Tb 1 0.04
Cm 2 0.08
Ex 0 0.00
Total 24 1.00
```
