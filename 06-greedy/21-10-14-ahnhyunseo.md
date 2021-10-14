## [leetcode 1353](https://leetcode.com/problems/maximum-number-of-events-that-can-be-attended/)

### 문제 설명
특정 기간 내에 최대한 많은 일정을 진행

### Input
events = [[1,2],[2,3],[3,4]]

### Output: 3

### Explanation:
You can attend all the three events.
One way to attend them all is as shown.
Attend the first event on day 1.
Attend the second event on day 2.
Attend the third event on day 3.


```javascript
function solution(events) {
    let answer=0
    let heap=new minHeap()

    events.sort((a,b)=>a[1]-b[1])
    let end=events[events.length-1][1]
    // 끝 부분 초기화

    events.sort((a,b)=>b[0]-a[0])
    let start=events[events.length-1][0]
    // 시작 부분 초기화
    // 시작 부분 초기화한대로 events 진행

    for(let i=start;i<=end;i++){
        // 시작부터 끝까지
        while(events.length && events[events.length-1][0]===i){
	// 현재 날짜에 시작하는 기간을 전부 넣어줌
            heap.insert(events.pop()[1])
        }
        let tmp=heap.get()
	// 기준값 하나 빼줌
        while(heap.size() && tmp<i) tmp=heap.get()
	// 마감이 가장 빠른 기간이지만, 마감이 지난 것일 경우, 다시 빼줌(while)
        if(tmp>=i) answer++
	// 기간에 부합할 경우에만 개수 증가
    }
    return answer
};
```
