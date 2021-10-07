# 문제
[ 백준 8958번 ]

[OX퀴즈](https://www.acmicpc.net/problem/8958)

# 풀이
```js
const fs = require("fs");
const filePath = process.platform ==='linux' ? '/dev/stdin' : './6_8958.txt';

let input = fs.readFileSync(filePath).toString().trim().split("\n");

let n = parseInt(input[0]);

// 각각의 문자열을 도는 함수 solve
const solve = (str) => {
    let score = 0;
    let scoreArr = new Array(str.length).fill(0);

    // 왼쪽에서 오른쪽으로 진행하면서 score에 +1해준다
    for(let i = 0; i < str.length; i++){
        // 삼항연산자 사용
        score = str[i] === "O" ? score + 1 : 0;
        scoreArr[i] = score;
    }

    // 배열의 합을 계산하기 위해 reduce()사용
    const result = scoreArr.reduce((prev, curr) => {
        return prev + curr;
    })

    return result;
}

// 각각 문자열을 돌기위한 for문
for(let i = 1; i <= n; i++){
    console.log(solve(input[i]));
}
```

## 사용한 js
- `parseInt()`: 정수형으로 변환
- `reduce`: 배열을 돌면서 처리한다. 리턴값을 다음 prev로 전달 (초기값을 화살표함수 뒤에 쉼표와 값으로 넣어줄 수 있다)

## Tastcase
```
5
OOXXOXXOOO
OOXXOOXXOO
OXOXOXOXOXOXOX
OOOOOOOOOO
OOOOXOOOOXOOOOX
```

## 결과
```
10
9
7
55
30
```