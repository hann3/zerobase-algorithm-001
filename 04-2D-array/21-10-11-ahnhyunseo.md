# 문제

[숫자 정사각형](https://www.acmicpc.net/problem/1051)

### 문제 설명
N*M크기의 직사각형이 있다. 각 칸은 한 자리 숫자가 적혀 있다.
이 직사각형에서 꼭짓점에 쓰여 있는 수가 모두 같은 가장 큰 정사각형을 찾는 프로그램을 작성하시오.
이때, 정사각형은 행 또는 열에 평행해야 한다.

### 제한 사항
- 각 칸의 숫자는 한 자리 수
- 첫 번째 줄에 N과 M이 주어짐
- N과 M은 50보다 작거나 같은 자연수
- 둘째 줄부터 N개의 줄에 수가 주어짐

### INPUT
3 5
42101
22100
22101

### OUTPUT
9

```javascript

const fs = require("fs");
const filePath = process.platform === 'linux' ? '/dev/stdin' : './testcase/1051.txt';

let input = fs.readFileSync(filePath).toString().trim().split("\n");

function solution(){
    let N = parseInt(input[0].split(' ')[0])
    let M = parseInt(input[0].split(' ')[1])
    // width, height
    
    let arr=new Array(N)
    // arr 선언
    let len = N > M ? M : N
    // 더 짧은 쪽을 기준으로 잡음(정사각형이기 때문에 한 변의 길이만 있어도 가능)
    for(let i = 1; i <= N ; i++) arr[i-1] = [...input[i].split('')]
    // arr 초기화
    // 문자열을 하나씩 잘라(0-9까지기 때문에 1개씩 잘라도 됨) 배열로 넣어줌
    
    for(let k=len;k>0;k--){
        // k는 최대 크기부터 줄여나감 (정사각형의 크기가 클 때부터 1이 될 때까지)
        for(let i=0;i<=N-k;i++){
            // N-k일 때, arr[N-k]부터 arr[N-k+k-1] 즉, arr[N-1]=제일 끝에 위치한 숫자까지 검사함
            for(let j=0;j<=M-k;j++){
                if(arr[i][j]===arr[i+k-1][j] && arr[i+k-1][j]===arr[i][j+k-1] && arr[i][j+k-1]===arr[i+k-1][j+k-1]) return k*k
                // 각 꼭지점의 숫자가 모두 같을 때, 한 변의 길이*길이 반환
                // 바로 return 해주는 이유: 길이가 클 때부터 돌았기 때문에 더 이상 큰 숫자가 나올 수 없음
                // k=1, 길이가 1이 되면 arr[0][0]에서 바로 return 되기 때문에 따로 if문 안 넣음
            }
        }
    }
}
console.log(solution())

```