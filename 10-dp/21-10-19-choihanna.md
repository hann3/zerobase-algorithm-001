
# 문제

[가장 높은 탑 쌓기](https://www.acmicpc.net/problem/2655) 

## 문제 설명 

밑면이 정사각형인 직육면체 벽돌들을 사용하여 탑을 쌓고자 한다. 탑은 벽돌을 한 개씩 아래에서 위로 쌓으면서 만들어 간다. 아래의 조건을 만족하면서 가장 높은 탑을 쌓을 수 있는 프로그램을 작성하시오.  

## 제한 사항  
  
* 벽돌은 회전시킬 수 없다. 즉, 옆면을 밑면으로 사용할 수 없다.
* 밑면의 넓이가 같은 벽돌은 없으며, 또한 무게가 같은 벽돌도 없다.
* 벽돌들의 높이는 같을 수도 있다.
* 탑을 쌓을 때 밑면이 좁은 벽돌 위에 밑면이 넓은 벽돌은 놓을 수 없다.
* 무게가 무거운 벽돌을 무게가 가벼운 벽돌 위에 놓을 수 없다.

## 입출력 예시
  
**입력**  

5  

25 3 4  

4 4 6  

9 2 3  

16 2 5  

1 5 2  
  
**출력** 
 
3  

5  

3  

1



# 구현 코드  

```javascript  

const fs = require('fs');
const filePath = process.platform === 'linux' ? '/dev/stdin' : './2655.txt';
let input = fs.readFileSync(filePath).toString().trim().split("\n");
const n = parseInt(input.shift().trim());
input = input.map(item => item.split(" ").map(item2 => +item2));

function solution(){
    let answer = [];
    let dy = new Array(n).fill(0) // 높이 배열
    let block = input;

    // 인덱스 번호를 정렬 전 미리 저장해야 함
    for(let i=0; i<n; i++){
        block[i].push(i+1);
    }

    block.sort((a, b)=>b[0]-a[0]); // 넓이에 따른 내림차순
    dy[0] = block[0][1]; 
    for(let i=1; i<n; i++){
        let max = 0;
        for(let j=i-1; j>=0; j--){
            // 밑에 있는 벽돌보다 무게가 작아야 함 
            if(block[j][2] > block[i][2] && dy[j] > max){
                max = dy[j];
            }
        }
            // 위 조건문을 거치지 않았을 경우 자기 자신의 높이 
            dy[i] = max + block[i][1];
    }
    let maxHeight = Math.max(...dy);
    for(let i=n-1; i>=0; i--){
        if(maxHeight === dy[i]) {
            maxHeight -= block[i][1];
            answer.push(block[i][3]); // index + 1 
        }
    }

    console.log(answer.length);
    for(let i=0; i<answer.length; i++) console.log(answer[i]);
}

solution();  

```
