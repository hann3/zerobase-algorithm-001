# 문제
[leet code 743 - Network Delay Time](https://leetcode.com/problems/network-delay-time/)

# 접근방향
- MinHeap을 이용해서 최소를 구해준다!
- 방문하지 않은 노드를 확인해서 전부 다 돌지 못하면 -1을 반환한다!

# 풀이
```js
class minHeap{
    constructor(){
        this.heap=[];
        this.heap.push([Number.MIN_SAFE_INTEGER, 0]);
    }
    insert([a, b]){
        this.heap.push([a, b]);
        this.upheap(this.heap.length-1);
    }
    upheap(pos){
        let temp=this.heap[pos];
        while(temp[1]<this.heap[parseInt(pos/2)][1]){
            this.heap[pos]=this.heap[parseInt(pos/2)];
            pos=parseInt(pos/2);
        }
        this.heap[pos]=temp;
    }
    get(){
        if(this.heap.length===2){
            return this.heap.pop();
        }
        let res;
        res=this.heap[1];
        this.heap[1]=this.heap.pop();
        this.downheap(1, this.heap.length-1);
        return res;
    }
    downheap(pos, len){
        let temp, i;
        temp=this.heap[pos];
        while(pos<=parseInt(len/2)){
            i=pos*2;
            if(i<len && this.heap[i][1]<this.heap[i+1][1]) i++;
            if(temp[1]<=this.heap[i][1]) break;
            this.heap[pos]=this.heap[i];
            pos=i;
        }
        this.heap[pos]=temp;
    }
    size(){
        return this.heap.length-1;
    }
    top(){
        return this.heap[1];
    }
}

var networkDelayTime = function(times, n, k) {
    let answer = 0;
    const heap = new minHeap();
    const graph = new Array(n + 1);
    for(let i = 1; i < n+1; i++){
        graph[i] = new Array();
    }
    // 해당 노드를 방문했는지 체크
    const check = new Array(n + 1).fill(0);
    // 거리를 저장하기 위한 배열
    const dist = new Array(n + 1).fill(10e9);

    for(const [a, b, c] of times){
        graph[a].push([b, c]);
    }

    // 초기값 할당
    dist[k] = 0;
    heap.insert([k, 0]);
    while(heap.size() > 0){
        let temp = heap.get();
        let now = temp[0];
        // 현재 노드를 방문한 노드라고 생각하고 check!
        check[now] = 1;
        let nowCost = temp[1];

        // 만약 dist에 저장되어 있는 값이 더 작으면 continue
        if(nowCost > dist[now]) continue;
        for(let [next, cost] of graph[now]){
            if(nowCost + cost < dist[next]){
                dist[next] = nowCost + cost;
                heap.insert([next, dist[next]]);
            }
        }
    }

    for (const d of dist){
        // 최대값을 구해줌
        if(10e9 !== d && d > answer){
            answer = d;
        }
    }
    // check배열을 확인 (방문하지 않은 노드가 있다면 answer는 -1을 할당
    for(let i = 1; i < n+1; i++){
        if(check[i] === 0)answer = -1;
    }
    return answer;
}
```

# 입력값
```
[[2,1,1],[2,3,1],[3,4,1]], 4, 2
```

# 출력
```
2
```