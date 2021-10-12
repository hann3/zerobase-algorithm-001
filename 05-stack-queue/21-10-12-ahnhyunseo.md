# 문제

[기능 개발](https://programmers.co.kr/learn/courses/30/lessons/42586?language=javascript)

### 문제 설명
- 각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다.
- 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 경우, 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포
- 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses
- 각 작업의 개발 속도가 적힌 정수 배열 speeds
- 각 배포마다 몇 개의 기능이 배포되는지를 return 

### 제한 사항
- 작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.
- 작업 진도는 100 미만의 자연수입니다.
- 작업 속도는 100 이하의 자연수입니다.
- 배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다. 예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.

### INPUT
**progresses**<br/>
[93, 30, 55]<br/>
[95, 90, 99, 99, 80, 99]<br/>

** speeds **<br/>
[1, 30, 5]<br/>
[1,1,1,1,1,1]<br/>

### OUTPUT
[2,1]<br/>
[1,3,2]<br/>

```javascript

function solution(progresses, speeds) {
    let answer = []
    let work = []
    for(let i=0;i<progresses.length;i++){
        work[i]=Math.ceil((100-progresses[i])/speeds[i])
    }
    // work === 작업 일수 list

    answer.push(0)
    // 각각 배포 가능한 개수
    let now_work=work[0]
    // 현재 작업 중인 기간
    for(let wk of work){
        if(now_work>=wk) answer.push(answer.pop()+1)
        // 현재 작업 중인 기간 내에 다음 일도 진행할 수 있다면
        // 기준 작업의 배포 개수 + 1 해줌
        else{
            answer.push(1)
            // 현재 작업은 따로 배포해야 함
            now_work=wk
            // 기준을 현재 작업으로 변경
        }
    }
    return answer
}

```