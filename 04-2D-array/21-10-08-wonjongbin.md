# 문제
[ 백준 1051번 ]

[숫자 정사각형](https://www.acmicpc.net/problem/1051)

# 문제요약
n*m 크기의 배열에서 가장 모서리(끝점이)의 수가 동일한 정사각형의 최대 넓이를 구하는 문제

# 접근방법
루프문을 두번 돌면서 각 수를 기준으로 동일하게 떨어진 곳의 숫자를 확인했다

# 풀이
```js
const fs = require("fs");
const filePath = process.platform === 'linux' ? '/dev/stdin' : './testcase/1051.txt';

let input = fs.readFileSync(filePath).toString().trim().split("\n");

const n = parseInt(input[0].split(" ")[0]);
const m = parseInt(input[0].split(" ")[1]);

// input 나눠주고, 숫자로
for(let i = 1; i < n+1; i++){
    input[i] = input[i].split("").map(item => +item);
}

let max = 1;
for(let i = 1; i < n; i++){
    for(let j = 0; j < m; j++){
        // 가장 큰 값부터 비교하기 위해
        cnt = Math.min(n-i, m-1-j); 
        // 하나의 값을 기준으로 오른쪽, 아래, 오른쪽아래를 확인
        while(cnt > 0){
            // 아래
            underCheck = input[i][j] === input[i+cnt][j];
            // 오른쪽
            rightCheck = input[i][j] === input[i][j+cnt];
            // 대각선
            diagonalCheck = input[i][j] === input[i+cnt][j+cnt];

            if(underCheck && rightCheck && diagonalCheck){
                // 정사각형의 크기중 최대값을 구함
                max = Math.max(max, (cnt+1)**2);
                break;
            }else {
                cnt--;
            }
        }
    }
}
console.log(max);
```

## Tastcase
```
3 5
42101
22100
22101
```

## 결과
```
9
```