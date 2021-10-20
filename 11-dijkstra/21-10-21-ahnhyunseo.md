```javascript
class DMinHeap{
    constructor(){
        this.heap=[]
        this.heap.push(-1e9)
    }
    insert(val){
        this.heap.push(val)
        this.upheap(this.heap.length-1) 
    }
    get(){
        if(this.heap.length===2) return this.heap.pop()
        if(this.heap.length===1) return false
        let res=this.heap[1]   
        this.heap[1]=this.heap.pop() 
        this.downheap(1, this.heap.length-1)   
        return res
    }
    size(){return this.heap.length-1}
    top(){return this.heap[1]}
    
    upheap(pos){
        let tmp=this.heap[pos] 
        while(tmp[1]<this.heap[parseInt(pos/2)][1]){
            this.heap[pos]=this.heap[parseInt(pos/2)]  
            pos=parseInt(pos/2) 
        }
        this.heap[pos]=tmp 
    }
    downheap(pos, len){
        let tmp=this.heap[pos], child
        while(pos<=parseInt(len/2)){  
            child=pos*2
            if(child<len && this.heap[child][1]>this.heap[child+1][1]) child++
            if(tmp[1]<=this.heap[child][1]) break
            this.heap[pos]=this.heap[child]
            pos=child
        }
        this.heap[pos]=tmp
    }
}
// ==== heap ====
var networkDelayTime = function(times, n, k) {
    let answer=0
    let heap=new DMinHeap()
    let graph=new Array(n+1)
    for(let i=0;i<=n;i++) graph[i]=[]
    for(let [start, end, time] of times) graph[start].push([end,time])
	// graph배열에 각 index에는 출발 지점, value에는 [도착, 시간] 추가
    let dist=new Array(n+1).fill(10e9)
	// 거리 저장할 배열(초기화는 큰 값으로 해줌)    

    dist[k]=0
	// k에서 시작하므로 k to k는 0
    heap.insert([k,0])
	// 시작 위치 추가
    while(heap.size()){
	// heap에 값이 존재할 동안
        let [start, total]=heap.get()
	// 시작하는 인덱스와 현재까지의 시간
        for(let [end, time] of graph[start]){
	// 현재 인덱스에서 출발하는 인덱스들 중
            if(total+time<dist[end]){
	// 시간이 단축된다면, 해당 값으로 저장해줌
                dist[end]=total+time
                heap.insert([end, dist[end]])
		// 현재 경로를 사용하기 위해 도착 인덱스와 시간 넣어줌
            }
        }
    }
    for(let i=1;i<=n;i++){
        if(dist[i]===10e9) return -1
	// 만약 도달할 수 없는 인덱스가 존재할 경우 -1 return
        answer=answer>dist[i]?answer:dist[i]
	// 최댓값 찾기
    }
    return answer
};





```