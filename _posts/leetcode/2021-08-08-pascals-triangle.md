---
title: "Leetcode Java Pascal's Triangle"
excerpt: "Leetcode Pascal's Triangle Java 풀이"
last_modified_at: 2021-08-08T15:55:00
header:
  image: /assets/images/leetcode/pascals-triangle.png
categories:
  - Leetcode
tags:
  - Programming
  - Leetcode
  - Java

toc: true
toc_ads: true
toc_sticky: true
use_math: true
---
# 문제
[Link](https://leetcode.com/pascals-triangle/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> generate(int numRows) {
    List<List<Integer>> result = new ArrayList<>();
    while (result.size() < numRows) {
      List<Integer> list = new ArrayList<>();
      list.add(1);
      if (result.size() > 1) {
        List<Integer> pre = result.get(result.size() - 1);
        for (int i = 1; i < result.size(); i++) {
          list.add(pre.get(i - 1) + pre.get(i));
        }
      }
      if (result.size() > 0) {
        list.add(1);
      }
      result.add(list);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/535120781/){:target="_blank"}

# 설명
1. 주어진 정수 numRows 높이의 [파스칼의 삼각형](https://ko.wikipedia.org/wiki/%ED%8C%8C%EC%8A%A4%EC%B9%BC%EC%9D%98_%EC%82%BC%EA%B0%81%ED%98%95){:target="_blank"}을 만드는 문제이다.

2. 결과를 저장하는 result의 크기가 파스칼의 삼각형 목표 높이인 numRows를 만족하지 않을 때까지 반복하여 주어진 정수 numRows 높이의 파스칼의 삼각형을 완성한다.
- 새 list를 생성하여 처음 값으로 1을 넣어 준다.
- 결과를 저장하는 result의 크기가 1보다 큰 경우, 아래를 수행한다.
  - 파스칼의 삼각형의 윗 층을 변수 pre에 넣어준다.
  - 1부터 결과를 저장한 result의 크기만큼 반복하여 변수 pre의 현재 위치의 -1번째 값과 현재 위치의 값의 합을 list에 넣어준다.
- 결과를 저장하는 result의 크기가 0이 아닌 경우, list에 1을 넣어 파스칼 삼각형의 한 줄을 완성해준다.
- 결과를 저장하는 result에 파스칼 삼각형의 한 줄을 만든 list를 넣어준다.

3. 반복문이 완료되면 파스칼의 삼각형을 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PascalsTriangle.java){:target="_blank"}에서 확인 가능합니다.