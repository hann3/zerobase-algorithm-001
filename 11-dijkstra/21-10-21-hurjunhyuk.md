# 문제

## leetcode - 743. Network Delay Time

reference: https://leetcode.com/problems/network-delay-time/

## 문제설명

You are given a network of n nodes, labeled from 1 to n. You are also given times, a list of travel times as directed edges times[i] = (ui, vi, wi), where ui is the source node, vi is the target node, and wi is the time it takes for a signal to travel from source to target.

We will send a signal from a given node k. Return the time it takes for all the n nodes to receive the signal. If it is impossible for all the n nodes to receive the signal, return -1.

## 입출력

```
Input: times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2
Output: 2
```
```
Input: times = [[1,2,1]], n = 2, k = 1
Output: 1
```
```
Input: times = [[1,2,1]], n = 2, k = 2
Output: -1
```

## 제한사항

- 1 <= k <= n <= 100
- 1 <= times.length <= 6000
- times[i].length == 3
- 1 <= ui, vi <= n
- ui != vi
- 0 <= wi <= 100
- All the pairs (ui, vi) are unique. (i.e., no multiple edges.)

## 작성 코드

```js
class minHeap {
	constructor() {
		this.heap = [];
		this.heap.push(Number.MIN_SAFE_INTEGER);
	}
	insert([a, b]) {
		this.heap.push([a, b]);
		this.upheap(this.heap.length - 1);
	}
	upheap(pos) {
		let tmp = this.heap[pos];
		while (tmp[1] < this.heap[parseInt(pos / 2)][1]) {
			this.heap[pos] = this.heap[parseInt(pos / 2)];
			pos = parseInt(pos / 2);
		}
		this.heap[pos] = tmp;
	}
	get() {
		if (this.heap.length < 2) return false;
		if (this.heap.length === 2) return this.heap.pop();
		let res = this.heap[1];
		this.heap[1] = this.heap.pop();
		this.downheap(1, this.heap.length - 1);

		return res;
	}
	downheap(pos, len) {
		let tmp = this.heap[pos];
		while (pos <= parseInt(len / 2)) {
			let child = pos * 2;
			if (child < len && this.heap[child][1] > this.heap[child + 1][1]) {
				child++;
			}
			if (tmp[1] <= this.heap[child][1]) {
				break;
			}
			this.heap[pos] = this.heap[child];
			pos = child;
		}
		this.heap[pos] = tmp;
	}
	size() {
		return this.heap.length - 1;
	}
}

// 다익스트라를 활용한 풀이
var networkDelayTime = function (times, n, k) {
	let answer = -1;
	// 최소힙을 사용해 노드에서 최단시간을 찾음
	let minH = new minHeap();
	// dist는 초기값으로 최대값 설정
	let dist = Array(n + 1).fill(6001);
	// graph에는 시작노드를 인덱스로 [도착노드, 소요시간] 세팅
	let graph = [...Array(n + 1)].map((e) => Array([]));
	for (const [from, to, time] of times) graph[from].push([to, time]);

	// 0번노드 0으로 초기화, 사용하지 않는 노드에 MAX값이 들어있으면
	dist[0] = 0;
	// 시작노드에서는 시작노드까지 시간은 0
	dist[k] = 0;
	minH.insert([k, 0]);
	// graph에 있는 모든 노드 정보를 탐색, 최소힙을 이용하여 dist정보를 갱신
	while (minH.size() > 0) {
		let tmp = minH.get();
		let now = tmp[0];
		let duration = tmp[1];
		// 최소힙에서 가져온 정보가 거리보다 클 경우 탐색할 필요 X
		if (duration > dist[now]) continue;
		// 힙에 들어있는 현재 노드 정보값으로 graph 탐색
		for (let [next, cost] of graph[now]) {
			// dist보다 작을 경우 값을 세팅해주면서 계속 탐색
			if (duration + cost < dist[next]) {
				dist[next] = duration + cost;
				minH.insert([next, dist[next]]);
			}
		}
	}
	// 모든 노드에 가는게 걸리는 시간이므로 dist에서 최대값을 구함
	for (const x of dist) {
		answer = Math.max(answer, x);
	}
	// 초기값이 그대로 남아있는 경우 도달하지 못한 것으로 판단하고 -1 리턴
	if (answer === 6001) return -1;
	return answer;
};
```
