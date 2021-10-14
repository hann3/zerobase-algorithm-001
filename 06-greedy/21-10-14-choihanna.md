# 문제 
[Maximum Number of Events That Can Be Attended](https://leetcode.com/problems/maximum-number-of-events-that-can-be-attended/)

## 아이디어(삽질 기록...)
> 최소 힙의 경우 스스로 구현하였지만 문제 해결에서 막혀 팀원들의 구현 방식을 많이! 참고하였음

☠ 실패한 원인 
- 처음 코드에서는 for문에서 마지막 이벤트가 끝나는 날을 기준으로 잡은 뒤 day를 1씩 감소시키는 방식으로 문제를 해결하려 하였지만 최소 힙의 특성을 고려하지 않은 이러한 접근 방식이 원인이었다
- 마감일을 기준으로 가장 개최가 가까운 이벤트에 참여하는 방식으로 구현하고 싶었으나 최소 힙을 사용하고 있다는 사실을 여러 번의 wrong 이후 깨달았다. 최소 힙에서는 가장 개최가 빠른 이벤트를 꺼내고, 가장 가까운(개최가 느린) 이벤트는 최소 힙에 그대로 남아 있어 answer가 증가되지 않는 문제가 발생했기 때문이다 (매우 기초적인!) 최대 힙을 사용하는 문제라면 이 방식이 가능했을 것 같다
- 개최일과 현재 day 사이의 거리를 계산하여 짧은 이벤트 먼저 참여하는 방식 역시 고민해 보았지만 복잡한 문제를 쉽게 해결하기 위해 최소힙을 사용하는 취지와 맞지 않는다고 생각하여 접근 방식을 반대로 바꾸었다
- 해당 자료구조를 사용하는 이유를 조금 더 고민하면서 방법을 세워야겠다. 


# 구현 코드 

```javascript

1. 최소힙 

class minHeap{
    constructor(){
        this.heap = [];
        this.heap.push(Number.MIN_SAFE_INTEGER);
    }
    insert(val){
        this.heap.push(val);
        this.upheap(this.heap.length-1);
    }

    upheap(pos){
        let tmp = this.heap[pos];
        while(tmp < this.heap[parseInt(pos/2)]){
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
            if(child < len && this.heap[child] > this.heap[child+1]) child++;
            if(this.heap[child] >= tmp) break;
            this.heap[pos] = this.heap[child];
            pos = child;
        }
        this.heap[pos] = tmp;
    }

}

2. 문제

function maxEvent(events){
    let answer = 0;
    let minH = new minHeap();
    events.sort((a, b)=>a[1]-b[1]); // 끝나는 날짜로 오름차순 
    let endDay = events[events.length-1][1];
    events.sort((a, b)=>a[0]-b[0]); // 시작하는 날짜로 오름차순
    let startDay = events[0][0];
    let i =0;
    for(let day = startDay; day <= endDay; day++){
        for(; i < events.length; i++){
            if(events[i][0] === day){ 
                minH.insert(events[i][1]);
            }
            else break;
        }
        if(minH.size()>0) {
            let deadline = minH.get();
            while(minH.size() !== 0 && deadline < day) deadline = minH.get();
            day <= deadline? answer++: true;
        }
    }
    return answer;
};

```

