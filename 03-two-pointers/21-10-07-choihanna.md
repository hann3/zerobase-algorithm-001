# 문제

[Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

## 문제설명

Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of the line i is at (i, ai) and (i, 0). Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

Notice that you may not slant the container.

> 컨테이너의 최대 넓이를 구해라 

## 제한 조건

* n == height.length
* 2 <= n <= 105
* 0 <= height[i] <= 104

## 입출력 예시


|height|output|
|------|------|
|[1,8,6,2,5,4,8,3,7]|49|
|[1,1]|1|
|[4,3,2,1,4]|16|
|[1,2,1]|2|


# 작성 코드 

```javascript

function solution(height){
    let left = 0;
    let right = height.length - 1;
    let maxArea = Number.MIN_SAFE_INTEGER;
    while (left < right) {
        /* 높이는 낮은 쪽에 맞춘다 */
        let _height = Math.min(height[left], height[right]); 
        /* 너비 = index */
        let _width = right - left; 
        let curArea = _height * _width;
        maxArea = maxArea < curArea? curArea: maxArea;
        height[left] < height[right]? left++: right--;
    }
    return maxArea;
}

```





