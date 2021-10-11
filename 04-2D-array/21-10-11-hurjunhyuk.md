# 문제

## boj - 숫자 정사각형(1051번)

reference: https://www.acmicpc.net/problem/1051

## 문제설명

N*M크기의 직사각형이 있다. 각 칸은 한 자리 숫자가 적혀 있다. 이 직사각형에서 꼭짓점에 쓰여 있는 수가 모두 같은 가장 큰 정사각형을 찾는 프로그램을 작성하시오. 이때, 정사각형은 행 또는 열에 평행해야 한다.

## 입력

첫째 줄에 N과 M이 주어진다. N과 M은 50보다 작거나 같은 자연수이다. 둘째 줄부터 N개의 줄에 수가 주어진다.

## 출력

첫째 줄에 정답 정사각형의 크기를 출력한다.

# 작성 코드

```js
// 파일로부터 값 입력 받기
const fs = require("fs");
const filePath = process.platform === 'linux' ? '/dev/stdin' : './testcase/1051.txt';
let input = fs.readFileSync(filePath).toString().trim().split("\n");
const n = parseInt(input[0].split(" ")[0]);
const m = parseInt(input[0].split(" ")[1]);
for (let i = 1; i < n + 1; i++) {
    input[i] = input[i].split("").map(item => +item);
}


// 테두리는 -1로 둘러침
let board = [...Array(n + 2)].map(e => Array(m + 2).fill(-1));

// ./testcase/1051.txt에서 받아온 값 n*m사이즈 board에 저장
// 해쉬에 board에 들어가는 숫자 개수 저장
let sH = new Map();
for (let i = 1; i < input.length; i++) {
    for (let j = 0; j < input[i].length; j++) {
        board[i][j + 1] = input[i][j];
        sH.set(input[i][j], (sH.get(input[i][j]) || 0) + 1);
    }
}

let answer = 1;
for (let i = 1; i < n; i++) {
    for (let j = 1; j < m; j++) {
        // 같은 숫자로 정사각형을 이루기 위해서는 최소 4개의 숫자가 필요
        if (sH.get(board[i][j]) < 4) {
            continue;
        }
        for (let k = 1; board[i + k][j + k] != -1; k++) {
            // 왼위 꼭지점 기준으로 오위 꼭지점과 비교
            if (board[i][j] !== board[i][j + k]) {
                continue;
            }
            // 왼위 꼭지점 기준으로 왼밑 꼭지점과 비교
            if (board[i][j] !== board[i + k][j]) {
                continue;
            }
            // 왼위 꼭지점 기준으로 오밑 꼭지점과 비교
            if (board[i][j] !== board[i + k][j + k]) {
                continue;
            }
            answer = Math.max(answer, (k + 1) ** 2);
        }
    }
}
console.log(answer);
```