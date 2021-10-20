
# 문제

[Network Delay Time](https://leetcode.com/problems/network-delay-time/) 

## 문제 설명 

You are given a network of n nodes, labeled from 1 to n. You are also given times, a list of travel times as directed edges times[i] = (ui, vi, wi), where ui is the source node, vi is the target node, and wi is the time it takes for a signal to travel from source to target.

We will send a signal from a given node k. Return the time it takes for all the n nodes to receive the signal. If it is impossible for all the n nodes to receive the signal, return -1.

> n개의 노드와 각 노드로 이동할 때 소요되는 시간이 담긴 times이 제공될 때, 노드 k에서 모든 노드로 신호를 전달하는 데에 걸리는 시간을 구하라. 단 모든 노드에게 전달할 수 없을 경우 -1을 반환한다.  


## 제한 사항  
  
* 1 <= k <= n <= 100
* 1 <= times.length <= 6000
* times[i].length == 3
* 1 <= u(i), v(i) <= n
* u(i) != v(i)
* 0 <= w(i) <= 100  

## 입출력 예시
  
|times|n|k|output|
|------|------|------|------|
|[[2,1,1], [2,3,1], [3,4,1]]|4|2|2|
|[[1,2,1]]|2|1|1|
|[[1,2,1]]|2|2|-1|


# 구현 코드  

```javascript 

1. 최소힙 

class minHeap{
    constructor(){
        this.heap = [];
        this.heap.push([Number.MIN_SAFE_INTEGER, 0]);
    }
    insert([a, b]){
        this.heap.push([a, b]);
        this.upheap(this.heap.length-1);
    }

    upheap(pos){
        let tmp = this.heap[pos];
        while(tmp[1] < this.heap[parseInt(pos/2)][1]){
            this.heap[pos] = this.heap[parseInt(pos/2)];
            pos = parseInt(pos/2);
        }
        this.heap[pos] = tmp;
    }
    size(){
        return this.heap.length -1;
    }

    get(){
        if(this.heap.length === 2) return this.heap.pop();
        let value = this.heap[1];
        this.heap[1] = this.heap.pop();
        this.downheap(1, this.heap.length-1);
        return value;  
    }
    downheap(pos, len){
        let tmp = this.heap[pos];
        while(pos <= parseInt(len/2)){
            let child = pos * 2;
            if(child < len && this.heap[child][1] > this.heap[child+1][1]) child++;
            if(this.heap[child][1] >= tmp) break;
            this.heap[pos] = this.heap[child];
            pos = child;
        }
        this.heap[pos] = tmp;
    }

}

2. 시간 계산 함수

const networkDelayTime = function(times, n, k) {
    let answer = 0;
    let minH = new minHeap();
    let graph = Array.from(Array(n+1), () => Array());
    // w의 최대값이 100이므로 101로 초기화 
    let dist = new Array(n+1).fill(101);
    for(let [start, end, time] of times){
        // 단방향 그래프 
        graph[start].push([end, time]);
    }
    dist[0] = 0;
    // k에서 출발하므로 k를 0으로 
    dist[k] = 0;
    minH.insert([k, 0]);
    while(minH.size() > 0){
        let tmp = minH.get();
        // k에서 이동할 노드, 소요 시간 
        let destination = tmp[0];
        let sendTime = tmp[1];
        if(sendTime > dist[destination]) continue;
        for(let [end, time] of graph[destination]){
            if(sendTime + time < dist[end]){
                dist[end] = sendTime + time;
                minH.insert([end, dist[end]]);
            }
        }
    }
    // 모든 노드로 전달할 수 없을 경우 -1을 반환
    // 방문하지 않은 노드는 초기값 101로 남아 있음 
    for(let i=1; i<=n; i++){
        if(dist[i] === 101) return -1;
    }

    // 모든 노드를 방문할 수 있는 시간이기 때문에 가장 큰 값을 반환  
    answer = Math.max(...dist);
    return answer;
};  

```
