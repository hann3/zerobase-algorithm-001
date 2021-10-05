# 문제

[완주하지 못한 선수](https://programmers.co.kr/learn/courses/30/lessons/42576)

### 문제 설명
마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

### 제한 사항
- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
- completion의 길이는 participant의 길이보다 1 작습니다.
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
- 참가자 중에는 동명이인이 있을 수 있습니다.

### INPUT
**participant**	**completion**
["leo", "kiki", "eden"]	["eden", "kiki"]
["marina", "josipa", "nikola", "vinko", "filipa"]	["josipa", "filipa", "marina", "nikola"]
["mislav", "stanko", "mislav", "ana"]	["stanko", "ana", "mislav"]

### OUTPUT
"leo"
"vinko"
"mislav"

# 작성 코드 

```javascript

function solution(participant, completion) {
    const marathon = new Map()
    for (let comp of completion) marathon.set(comp, (marathon.get(comp) || 0) + 1)
    /* marathon에 '완주한 선수 이름': '인원 수'를 넣어줌 */
    for (let part of participant){
        if (!marathon.has(part) || marathon.get(part) === 0) return part
        /* marathon에 없거나, 값이 0일 경우(동명인 사람 모두 통과) 해당 참가자 return */
        else marathon.set(part, marathon.get(part)-1)
        /* 동명이인이 있을 수 있기 때문에 value인 인원 수를 1씩 감소시킴 */
    }
}

```