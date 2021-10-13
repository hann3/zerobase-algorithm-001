# 문제
[Maximum Number of Events That Can Be Attended](https://leetcode.com/problems/maximum-number-of-events-that-can-be-attended/)

# 접근방향
Minheap을 사용해서 조건에 맞을때 counting!

# 풀이
```js
class MinHeap{
    constructor(){
        this.heap = [];
        this.heap.push(0);
    }
    size = () => {
        return this.heap.length - 1;
    }

    insert = (value) => {
        this.heap.push(value);
        this.upheap(this.heap.length-1);
    }
    
    upheap = (pos) => {
        let temp = this.heap[pos];

        while(temp < this.heap[parseInt(pos/2)]){
            this.heap[pos] = this.heap[parseInt(pos/2)];
            pos = parseInt(pos/2);
        }
        this.heap[pos] = temp;
    }

    get = () => {
        if(this.size() === 0) return false;
        if(this.size() === 1) return this.heap.pop();
        const result = this.heap[1];
        this.heap[1] = this.heap.pop();
        this.downheap(1, this.heap.length-1);
        return result;
    }

    downheap = (pos, len) => {
        let temp = this.heap[pos];
        let child;

        while(pos <= parseInt(len/2)){
            child = pos * 2;
            if(child < len && this.heap[child] > this.heap[child + 1]) child++;
            if(temp <= this.heap[child]) break;

            this.heap[pos] = this.heap[child];
            pos = child;
        }
        this.heap[pos] = temp;
    }

}

const maxEvents = (events) => {
    // 시작일을 기준으로 정렬
    events.sort((a, b) => a[0]-b[0]);
    const heap = new MinHeap();
    
    let cnt = 0;
    let i = 0;
    // day의 범위만큼 1 < day < 10e5
    for(let day = 1; day < 10e5; day++){
        // events의 i는 누적
        for( ; i < events.length; i++){
            // events[i]의 시작값이 같을때 insert 
            if(events[i][0] !== day) break;
            heap.insert(events[i][1]);
        }
        // heap에 끝나는 날짜가 남아있을때
        if(heap.size() > 0){
            // 끝나는 날짜가 현재일보다 크면 카운팅  
            if(heap.get() >= day) cnt++;
            // 아니면 cnt를 임시저장하고 그날에 event를 참여할 수 있도록 현재일보다 큰값이 나올때까지 get
            else {
                cnt_temp = cnt;
                while(heap.size() > 0 && cnt_temp === cnt){
                    if(heap.get() >= day) cnt++;
                }
            }
        }
    }
    return cnt;
}
```

# 입력값
```
[[1,2],[2,3],[3,4]]
[[1,2],[2,3],[3,4],[1,2]]
[[1,4],[4,4],[2,2],[3,4],[1,1]]
[[1,1],[1,2],[1,3],[1,4],[1,5],[1,6],[1,7]]
[[1,2],[1,2],[3,3],[1,5],[1,5]]
[[1,2],[1,2],[1,6],[1,2],[1,2]]
[[1,5],[1,5],[1,5],[2,3],[2,3]]
[[1,10],[2,2],[2,2],[2,2],[2,2]]
```
# 출력
```
3
4
4
7
5
3
5
2
18
```