# 문제

## leetcode - 39. Combination Sum

reference: https://leetcode.com/problems/combination-sum/

## 문제설명

Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.

The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is guaranteed that the number of unique combinations that sum up to target is less than 150 combinations for the given input.

-> 순열 문제: candidates라는 배열이 주어지면 배열의 요소로 합이 7이 되는 배열들을 리턴하는 함수를 작성하는 문제. candidates의 배열의 요소는 중복으로 사용 가능.

## 입출력

|candidates|target|output|
|----|----|----|
|[2,3,6,7]|7|[[2,2,3], [7]]|
|[2,3,5]|8|[[2,2,2,2],[2,3,3],[3,5]]|
|[2]|1|[]|
|[1]|1|[1]|
|[1]|2|[1,1]|


## 작성 코드

### 첫번째 접근 방법 (실패)

- DFS를 이용하여 요소의 합이 target에 일치하는 경우 answer에 담되, 집합 자료형 set을 이용하여 중복이 생기지 않도록 했음.
- candidates가 `[2, 3, 6, 7]`이고 target이 `7`인 경우 output이 `[[2, 2, 3], [7]]`이 되어야 하나 `{[ 2, 2, 3 ], [ 2, 2, 3 ], [ 2, 2, 3 ], [ 2, 2, 3 ], [ 2, 2, 3 ], [ 2, 2, 3 ], [ 2, 2, 3 ],   [ 7 ]}`이 나와버림
- 첫번째 시도에서는 DFS 내부 for loop의 시작점을 0번 인덱스로 하고 배열에 모두 담은 뒤 배열의 합이 target이 되는 것 중에서 중복을 제거하는 방식으로 구현해서 실패함. 애초에 중복이 되지 않는 방식으로 배열에 담아야 할 듯?

```js
var combinationSum = function (candidates, target) {
	let answer = new Set();
	let tmp = [];

	function sumOfElements(nums) {
		let sum = 0;

		for (let n of nums) {
			sum += n;
		}
		return sum;
	}
	function DFS(tmp) {
		if (sumOfElements(tmp) > target) return;
		if (sumOfElements(tmp) === target) {
			tmp.sort((a, b) => a - b);
			answer.add(tmp.slice());
			return;
		}
		for (let i = 0; i < candidates.length; i++) {
			tmp.push(candidates[i]);
			DFS(tmp);
			tmp.pop();
		}
	}
	DFS(tmp);
	return answer.size;
};
```

### 두번째 접근 방법 (성공)

- 일단 모두 담고 배열의 합이 target과 일치하는 경우, 중복을 제거하는 첫번째 방식이 제대로 동작하지 않아서 배열에 담을 때부터 중복이 발생하지 않도록 구현을 시도함
- DFS 내부 for loop에서 시작 인덱스를 0이 아닌 현재 인덱스로 하여 DFS 탐색을 하도록 구현함.

```js
var combinationSum = function (candidates, target) {
	let answer = [];
	let tmp = [];

	function sumOfElements(nums) {
		let sum = 0;

		for (let n of nums) {
			sum += n;
		}
		return sum;
	}
	function DFS(tmp, s) {
		if (sumOfElements(tmp) > target) return;
		if (sumOfElements(tmp) === target) {
			tmp.sort((a, b) => a - b);
			answer.push(tmp.slice());
			return;
		}
		for (let i = s; i < candidates.length; i++) {
			tmp.push(candidates[i]);
			DFS(tmp, i);
			tmp.pop();
		}
	}
	DFS(tmp, 0);
	return answer;
};
```