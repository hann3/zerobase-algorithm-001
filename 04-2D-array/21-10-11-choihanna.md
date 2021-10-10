# 문제
[숫자 정사각형](https://www.acmicpc.net/problem/1051)

# 문제설명 
N*M크기의 직사각형이 있다. 각 칸은 한 자리 숫자가 적혀 있다. 이 직사각형에서 꼭짓점에 쓰여 있는 수가 모두 같은 가장 큰 정사각형을 찾는 프로그램을 작성하시오. 이때, 정사각형은 행 또는 열에 평행해야 한다.

## 입출력 예시

|input|output|
|------|------|
|3 5 42101 22100 22101|9|

## Tip
💡 변수를 선언하는 방법에는 (1) 생성자 함수 호출 new Array( ) (2) 리터럴 [ ] 두 가지 방식이 존재
* 리터럴을 사용하는 편이 직관적이고 속도면에서 유리하여 권장된다   


## 작성 코드

```javascript

const fs = require("fs");
const filePath = process.platform === 'linux' ? '/dev/stdin' : './testcase/1051.txt';
let input = fs.readFileSync(filePath).toString().trim().split("\n");

function solution(){
    const n = parseInt(input[0].split(" ")[0]);
    const m = parseInt(input[0].split(" ")[1]);
    const maxSize = Math.min(n, m); // 최대 정사각형 크기 <= min(m, m)
    let maxArea = 0;
    let arr = [];
    for(let i=1; i<= n; i++) arr[i-1] = [...input[i].split("")];
    for(let i=0; i<n; i++){
        for(let j=0; j<m; j++){
            for(let k=1; k< maxSize; k++){
                // 경계처리 
                if(!(i + k < n && j + k < m)) break;
                let current = arr[i][j];
                // 아래, 오른쪽, 대각선 차례로 비교
                if(current === arr[i+k][j] && current === arr[i][j+k] && current === arr[i+k][j+k]) maxArea = maxArea < k? k: maxArea;
            } 
        }
    }
    return Math.pow(maxArea+1, 2);
}

console.log(solution());

```