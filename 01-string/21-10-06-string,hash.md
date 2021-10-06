---
title:  "[Algorithm] String, Hash"
excerpt: "String, Hash 알고리즘 정리"

categories:
  - Algorithm
tags:
  - [Algorithm]

toc: true
toc_sticky: true
 
date: 2021-10-06
last_modified_at: 2021-10-06
---

# String 
문자열을 다루는 알고리즘을 풀면서 알게된 방법

## 1. 앞 뒤 문자열의 비교

> 문자열이 주어지고 각 알파벳이 몇개가 이어지는지 모든 개수를 출력해보는 문제(1개도 출력)

```js
str = "aaazbbbccc";

// 공백을 추가해주는 이유는 마지막에 종료하기 위해서
str = str + ""

// 몇개나 중복되는지 체크하기 위해서(기본적으로 한개는 존재하므로 1)
cnt = 1;
for (let i = 0; i < str.length; i++){
  if(str[i] === str[i+1]){
    cnt++;
  }else {
    console.log(`${str[i]}은 ${cnt}개 있습니다`)
    cnt = 1;
  }
}
```

**index**를 이용해서 현재 index와 그 다음번의 index를 비교해본다

마지막 index에서는 다음번에 비교할 문자가 없기때문에 미리 공백을 추가해준다(`str = str + " "`)


## 2. 문자열을 앞 뒤로 비교해주는 방법 

index를 이용해서 제일 처음 인덱스 `left`, 맨 마지막을 가르키는 `right`를 지정한다
```js
left = 0;
right = str.length-1;
// index를 이용하기 때문에 -1을 해준다
```
이후 문자열을 확인하면서 +1, -1을 해주면서 다시 확인한다 
- `left`는 +1(→ 방향)
- `right`는 -1(← 방향) 

\* **문제타입**  
\- 문자열에서 문자뒤집기  
\- 회문문자열
{: .notice}

## 3. 문자열에서의 브루트포스
브루트포스(brute force)란, **완전탐색 알고리즘**이다

가능한 모든 경우의 수를 확인하면서 요구에 충족되는 조건을 리턴할 수 있다 (100% 정답만을 리턴)

> 같은 문자열이 존재하는가를 확인하는 문제

```js
strArr = ["abc", "abcd", "efg", "abc"];
const n = strArr.length;

const check = (strArr, n) => {
  // 반복문의 중첩을 통해 모든 경우의 수를 확인한다 (문자열 4개 기준 - 6가지)
  for (let i = 0; i < n; i++){        // n은 문자열을 담고있는 배열의 길이
    for (let j = i+1; j < n; j++ ){     // n은 문자열을 담고있는 배열의 길이
      if(staArr[i] === strArr[j]){    
        return false;   // 같은 문자열이 있을때 false를 리턴
      }
    }
  }
  return true;    // 반복문동안 false 리턴이 수행되지 않은 경우 중복되는 문자열이 없었다고 판단 (true 리턴)
}
```

반복문의 중첩을 사용해서 **모든 경우를 확인한다**

두번째 `for`문에서 `j`가 `i+1`에서부터 시작하는 이유는 이전의 문자열과의 비교는 이전에 수행되었기 때문이다s

| i | j | str |
|:---:|:---:|:---:|
| 0 | 1 | `abc`, `abcd` |
| 0 | 2 | `abc`, `efg` |
| 0 | 3 | `abc`, `abc` |
| 1 | 2 | `abcd`, `efg` |
| 1 | 3 | `abcd`, `abc` |
| 2 | 3 | `efg`, `abc` |
 
<br>

# Hash
해시테이블과 반복문 등을 사용해서 값의 누적, 중복의 여부 등을 확인할 수 있다

## 해시 테이블(Hash Table)
자료구조의 종류 중 하나로 **key**와 **value**를 가지는 자료구조 형태이다

- Hash Function을 이용해서 빠른 접근이 가능하다 (시간복잡도: O(n))
- Map의 사용
  ```js
  const hashTable = new Map();
  ```

## 1. Map.set()
값을 설정하는 해시테이블(Map)의 함수
```js
const hashTable = new Map();

hashTable.set("key", "value");

console.log(hashTable);
```
```
// 결과
Map { 'key' => 'value' }
```
`set()`에 두개의 인자를 넣는다 

- 첫번째 인자: key
- 두번째 인자: value
- 인자를 하나만 넣을 경우 인자는 key값이 되고 value는 `undefined`

## 2. Map.get()
선언한 Map에서 값을 가져오는 해시테이블의(Map)의 함수
```js
const hashTable = new Map();

hashTable.set("서울", "서울특별시");
hashTable.set("수원", "그냥 수원시");

console.log(hashTable.get("서울"));
console.log(hashTable.get("수원"));
```
```
// 결과
서울특별시
그냥 수원시
```
`get()`의 인자로 한개를 넣어주게 되는데 이때 **key값**이 들어가게 된다

## 3. Map.has()
선언한 Map에 **key**가 존재하는지를 확인하는 함수

```js
const hashTable = new Map();

hashTable.set("서울", "서울특별시");
hashTable.set("수원", "그냥 수원시");

console.log(hashTable.has("서울"));
console.log(hashTable.has("제주도"));
```
```
// 결과
true
false
```

## 4. Map.delete()
선언된 Map에서 key로 key와 value를 삭제하는 함수
```js
const hashTable = new Map();

hashTable.set("서울", "서울특별시");
hashTable.set("수원", "그냥 수원시");

hashTable.delete("수원");

console.log(hashTable);
```
```
// 결과
Map { '서울' => '서울특별시'}
```
- `true`, `false`를 리턴한다

## 5. Map.size()
Map의 크기를 리턴하는 함수
```js
const hashTable = new Map();

hashTable.set("서울", "서울특별시");
hashTable.set("수원", "그냥 수원시");

console.log(hashTable.size);
```
```
// 결과
2
```
- 빈 Map의 size를 출력하면 0

<br>

# JS 메소드

## 1. split()
문자열(string)을 지정한 구분자로 구분한다
```js
문자열.split("구분자");
```

> [MDN Link](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/split)

```js
// 예시
const str = "a, b, c, d, e";
arr = str.split(", ");

console.log(arr);
``` 
```
// 결과
[ 'a', 'b', 'c', 'd', 'e' ]
```

## 2. join()
배열의 모든 요소를 나열해 하나의 문자열(string)로 만든다
```js
배열.join("각 항목 사이에 지정할 문자열")
```

> [MDN Link](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/join)

```js
// 예시
const arr =  [ "a", "b", "c", "d", "e" ];

str = arr.join("");
console.log(str);
```
```
// 결과
abcde
```

## 3. substring()
문자열(string)의 인덱스를 사용해서 시작인덱스부터 끝인덱스까지의 부분문자열을 반환한다

```js
문자열.substring(시작인덱스, 끝인덱스)
```

> [MDN Link](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/substring)

```js
const str = "abcdefg";
const subStr = str.substring(1, 4);

console.log(subStr);
```
```
// 결과
bcd
```
- 만약 끝인덱스를 입력하지 않은경우 끝까지 진행한다

## 4. sort()
배열을 정렬해준다
```
배열.sort();
```

> [MDN Link](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

```js
const arr = [1, 3, 2, 4];
const arr2 = ["a", "c", "d", "b"];

arr.sort((a, b) => a-b);
arr2.sort();

console.log(arr);
console.log(arr2);
```
```
// 결과
[ 1, 2, 3, 4 ]
[ 'a', 'b', 'c', 'd' ]
```

- **복사본을 생성하지 않고 원본이 변경된다**
- 기본적으로 문자열의 유니코드 코드에 따라 정렬한다 (숫자의 오름차순 정렬시 1, 2, 11가 있다면 1, 11, 2로 정렬됨)
- 오름차순의 경우(`arr.sort((a,b) => a-b)`)
- 내림차순의 경우(`arr.sort((a,b) => b-a)`)


## 5. reverse()
배열의 순서를 반대로 반전시켜준다

```js
배열.reverse();
```

> [MDN Link](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)

```js
const arr = [1, 2, 3, 4];
arr.reverse();

console.log(arr);
```
```
// 결과
[ 4, 3, 2, 1 ]
```

## 6. isNaN()
인자가 숫자인지 아닌지 false, true값을 반환한다
```js
console.log(isNaN(1));
```
```
// 결과
false
```

- 숫자이면 false반환
- 숫자가 아니면 true 반환
