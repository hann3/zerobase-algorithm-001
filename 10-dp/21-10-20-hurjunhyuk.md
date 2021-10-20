# 문제

## boj - 가장높은탑쌓기

reference: https://www.acmicpc.net/problem/2655

## 문제설명

밑면이 정사각형인 직육면체 벽돌들을 사용하여 탑을 쌓고자 한다.
탑은 벽돌을 한 개씩 아래에서 위로 쌓으면서 만들어 간다.
아래의 조건을 만족하면서 가장 높은 탑을 쌓을 수 있는 프로그램을 작성하시오.

1. 벽돌은 회전시킬 수 없다. 즉, 옆면을 밑면으로 사용할 수 없다.
2. 밑면의 넓이가 같은 벽돌은 없으며, 또한 무게가 같은 벽돌도 없다.
3. 벽돌들의 높이는 같을 수도 있다.
4. 탑을 쌓을 때 밑면이 좁은 벽돌 위에 밑면이 넓은 벽돌은 놓을 수 없다.
5. 무게가 무거운 벽돌을 무게가 가벼운 벽돌 위에 놓을 수 없다.

## 입력

첫째 줄에는 입력될 벽돌의 수가 주어진다. 입력으로 주어지는 벽돌의 수는 최대 100개이다.
둘째 줄부터는 각 줄에 한 개의 벽돌에 관한 정보인 벽돌 밑면의 넓이, 벽돌의 높이 그리고 무게가 차례대로 양의 정수로 주어진다.
각 벽돌은 입력되는 순서대로 1부터 연속적인 번호를 가진다. 벽돌의 넓이, 높이 무게는 10,000보다 작거나 같은 자연수이다.

## 출력

탑을 쌓을 때 사용된 벽돌의 수를 빈칸없이 출력하고,
두 번째 줄부터는 탑의 가장 위 벽돌부터 가장 아래 벽돌까지 차례로 한 줄에 하나씩 벽돌 번호를 빈칸없이 출력한다.

## 작성 코드

```js
// 파일로부터 값 입력 받기
const fs = require("fs");
const filePath =
	process.platform === "linux" ? "/dev/stdin" : "./testcase/2655.txt";
let input = fs.readFileSync(filePath).toString().trim().split("\n");

// 벽돌 개수 세팅
const n = parseInt(input[0].split(" ")[0]);
// 넓이, 높이, 무게 세팅
let bricks = [];
for (let i = 1; i < n + 1; i++) {
	bricks[i - 1] = input[i].split(" ").map((item) => +item);
}
// enumㅁ
const AREA = 0;
const HEIGHT = 1;
const WEIGHT = 2;
const INDEX = 3;

// dp table은 i번째 벽돌을 포함하는 최대 높이
let dy = Array(bricks.length);
for (let i = 0; i < bricks.length; i++) {
	bricks[i].push(i + 1);
}

// 넓이 기준으로 내림차순 정렬
bricks.sort((a, b) => b[AREA] - a[AREA]);

// idx에는 높이의 합이 최대가 되는 벽돌들의 인덱스 값이 들어감
let idx = Array(bricks.length);
for (let i = 0; i < bricks.length; i++) {
	idx[i] = Array(1).fill(bricks[i][INDEX]);
}

// 전체 벽돌들을 탐색하면서 dy, idx에 값을 세팅
// dy === i번째 벽돌을 포함하는 높이의 합의 최대
// idx === 높이의 합의 최대일 때의 벽돌의 index 번호 (1 ~ N)
for (let i = 0; i < bricks.length; i++) {
	// 현재 벽돌을 포함해야 하므로 초기값으로 현재 벽돌 높이 설정
	dy[i] = bricks[i][HEIGHT];
	// 현재 인덱스의 벽돌을 포함하는 벽돌들의 높이의 합의 최대값, 그 벽돌들의 인덱스 번호를 세팅
	for (let j = 0; j < i; j++) {
		// 앞에 있는 벽돌이 더 가벼우면 continue (넓이를 내림차순으로 정렬해둠, === 포함해도 조건에 의해 결과는 같음)
		if (bricks[i][WEIGHT] > bricks[j][WEIGHT]) continue;
		// 높이의 합이 최대가 안될 경우 continue
		if (dy[i] >= dy[j] + bricks[i][HEIGHT]) continue;

		// dy에 높이 합을 갱신하고
		dy[i] = dy[j] + bricks[i][HEIGHT];
		// 가장 가벼운 현재 벽돌의 인덱스를 저장
		idx[i] = [bricks[i][INDEX]];
		// 앞에서 찾은 벽돌들의 인덱스를 저장
		for (const x of idx[j]) {
			idx[i].push(x);
		}
	}
}

let answer = [];
let height = Number.MIN_SAFE_INTEGER;
// 최대 높이값으로 갱신해 나가면서 그에 해당하는 벽돌 인덱스 번호를 세팅
for (let i = 0; i < dy.length; i++) {
	if (height >= dy[i]) continue;
	answer = idx[i];
	height = dy[i];
}

// 정답출력: 길이, 벽돌 인덱스
console.log(answer.length);
for (const x of answer) console.log(x);
```
