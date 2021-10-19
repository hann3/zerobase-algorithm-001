# 문제
[백준(2655)-가장높은탑쌓기](https://www.acmicpc.net/problem/2655)

# 접근방향
높이를 기준으로 동적프로그래밍을 활용!

# 풀이
```js
const fs = require('fs');
const filePath = process.platform === 'linux' ? '/dev/stdin' : './testcase/2655.txt';

let input = fs.readFileSync(filePath).toString().trim().split("\n");
const n = parseInt(input.shift().trim());
input = input.map(item => item.trim().split(" ").map(item2 => +item2));

const solve = (n, arr) => {
    const dy = new Array(n).fill(0);
    // 벽돌의 index를 넣어줄 배열
    const blockArr = [];
    
    // index를 넣어줌
    for(let i = 0; i < n; i++){
        arr[i].push(i+1);
    }
    
    // 넓이를 기준으로 정렬
    arr.sort((a, b) => b[0] - a[0]);
    // 첫값을 넣어준다(높이)
    dy[0] = arr[0][1];
    
    for(let i = 0; i < n; i++){
        for(let j = 0; j < i; j++){
            if(arr[i][2] < arr[j][2]){
                // 높이를 더한것과 더하지 않은 것을 비교
                dy[i] = Math.max(dy[j]+arr[i][1], dy[i]);
            }
        }
        // 만약 위 if문에 걸리지 않았다면 자신의 높이
        if(dy[i] === 0) dy[i] = arr[i][1];
    }
    // 가장 높은 탑을 max로 찾는다
    let maxHeight = Math.max(...dy);
    // index를 찾아야하기 때문에 거꾸로 찾아준다 (빼면서)
    for(let i = n-1; i >= 0; i--){
        if(maxHeight === dy[i]){
            blockArr.push(arr[i][3]);
            maxHeight -= arr[i][1];
        }
    }
    return blockArr;
}
let answer = solve(n, input);
console.log(answer.length);
for(let a of answer){
    console.log(a);
}
```

# 입력값
```
5
25 3 4
4 4 6
9 2 3
16 2 5
1 5 2
```

# 출력
```
3
5
3
1
```