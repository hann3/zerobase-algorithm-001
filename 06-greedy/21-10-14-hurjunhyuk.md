# 문제

## leetcode - 1353. Maximum Number of Events That Can Be Attended

reference: https://leetcode.com/problems/maximum-number-of-events-that-can-be-attended/

## 문제설명

iven an array of events where events[i] = [startDayi, endDayi]. Every event i starts at startDayi and ends at endDayi.

You can attend an event i at any day d where startTimei <= d <= endTimei. Notice that you can only attend one event at any time d.

Return the maximum number of events you can attend.

## 입출력

|input|output|
|----|----|
|[[1,2],[2,3],[3,4]]|3|
|[[1,2],[2,3],[3,4],[1,2]]|4|
|[[1,4],[4,4],[2,2],[3,4],[1,1]]|4|
|[[1,100000]]|1|
|[[1,1],[1,2],[1,3],[1,4],[1,5],[1,6],[1,7]]|7|

## 작성 코드

```js
class minHeap {
    constructor() {
        this.heap = [];
        this.heap.push(Number.MIN_SAFE_INTEGER);
    }
    insert(val) {
        this.heap.push(val);
        this.upheap(this.heap.length - 1);
    }
    upheap(pos) {
        let tmp = this.heap[pos];
        while (tmp < this.heap[parseInt(pos/2)]) {
            this.heap[pos] = this.heap[parseInt(pos/2)];
            pos = parseInt(pos/2);
        }
        this.heap[pos] = tmp;
    }
    get() {
        if (this.heap.length < 2) {
            return false;
        }
        let res;
        if (this.heap.length > 2) {
            res = this.heap[1];
            this.heap[1] = this.heap.pop();
            this.downheap(1, this.heap.length - 1);
        } else {
            res = this.heap.pop();
        }
        return res;
    }
    downheap(pos, len) {
        let tmp = this.heap[pos];
        while (pos <= parseInt(len/2)) {
            let child = pos * 2;
            if (child < len && this.heap[child] > this.heap[child + 1]) {
                child++;
            }
            if (tmp <= this.heap[child]) {
                break;
            }
            this.heap[pos] = this.heap[child];
            pos = child;
        }
        this.heap[pos] = tmp
    }
    size() {
        return this.heap.length - 1;
    }
}

var maxEvents = function(events) {
    let answer = 0;
    // 시작 날짜를 기준으로 오름차순 정렬
    events.sort((a, b) => {
        if (a[0] === b[0])
            return a[1] - b[1];
        else
            return a[0] - b[0];
    });
    // 가장 늦게 끝나는 종료날짜
    const maxDay = [...events].sort((a,b) => b[1] - a[1])[0][1];
    let minH = new minHeap();

    let i = 0;
    for (let day = 1; day <= maxDay; day++) {
        // event 시작날짜가 현재날짜보다 같거나 작은 경우만 minHeap에 넣어줌
        for (; i < events.length; i++) {
            if (events[i][0] > day) {
                break;
            }
            minH.insert(events[i][1]);
        }
        let tmp;
        // minHeap에서 가져온 종료 날짜가 현재 날짜보다 작은 경우 날려버림
        while(minH.size() && (tmp = minH.get()) < day) {
            ;
        }
        // minHeap에서 가져온 종료 날짜가 현재 날짜보다 클 때 answer 증가
        if (tmp >= day)
            answer++;
        // events 전부 minHeap에 넣었고, minHeap이 비어있을 때 더이상 반복할 필요 없음
        if (i === events.length && minH.size() === 0) {
            break;
        }
    }
    return answer;
};
```
