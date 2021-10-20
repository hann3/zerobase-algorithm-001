# [애증의 가장 높은 탑 쌓기](https://www.acmicpc.net/problem/2655)

```javascript
const fs = require('fs');
const filePath = process.platform === 'linux' ? '/dev/stdin' : './test2.txt';

let input = fs.readFileSync(filePath).toString().trim().split("\n");
const n = parseInt(input.shift().trim());
arr = input.map(item => item.split(" ").map(item2 => +item2));

if(n===0) return console.log(0)

let answer=0
for(let i=0;i<n;i++) arr[i].push(i+1)

arr.sort((a,b)=>b[0]-a[0])
// 넓이, 무게 순으로 정렬

let dp=new Array(n).fill(0)
// 누적 높이를 넣을 배열
let top=new Array(n)
// 누적 index 추가
for(let i=0;i<n;i++){
    dp[i]=0
    top[i]=[]
}

dp[0]=arr[0][1]
top[0].push(arr[0][3])
// 맨 하단 값 초기화

for(let i=1;i<n;i++){
    let tmp=0, idx=-1
    for(let j=i-1;j>=0;j--){
        if(arr[j][2]>arr[i][2] && dp[j]>tmp){
	// 상단에 놓을 수 있는 값들 중 높이가 가장 큰 값의 정보 저장
            tmp=dp[j]
            idx=j
        }
    }
    dp[i]=tmp+arr[i][1]
	// 누적 높이 저장
    if(idx!=-1) top[i].push(...top[idx],arr[i][3])
	// if문을 통과했을 때
	// 이전까지 블록의 인덱스와 본인의 인덱스를 top에 추가
    else top[i].push(arr[i][3])
	// 본인보다 큰 블록이 없을 경우, 본인의 인덱스만 추가
    answer=dp[answer]<dp[i]?i:answer
	// 항상 가장 높은 블록들의 index를 answer에 저장
}
console.log(top[answer].length)
// 인덱스 answer의 블록 개수(저장된 index 개수)를 추력
for(let i of top[answer].reverse()) console.log(i)
// 각 index를 상단부터 출력

```