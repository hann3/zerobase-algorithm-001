# 문제

[전화번호 목록](https://programmers.co.kr/learn/courses/30/lessons/42577)


전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

* 구조대 : 119
* 박준영 : 97 674 223
* 지영석 : 11 9552 4421

전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.


# 작성 코드 

```javascript

function solution(phone_book){
    phone_book.sort();
    /* 
    문자열 순서 기본 정렬 
    ex) 12 123 1235 678
    */
    for(let i = 1; i < phone_book.length; i++){
        let prefix = phone_book[i-1].length;
        /*  prefix의 length만큼만 비교  */
        /*  Array.prototype.slice(st, ed): 배열 복사 (실제 배열 변경 x) */
        /*  String.prototype.slice(st, ed) */ 
        if (phone_book[i-1].slice(0, prefix) === phone_book[i].slice(0, prefix)) return false;
    }
    return true;

}

```
