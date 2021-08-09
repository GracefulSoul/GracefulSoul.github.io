---
title: "Leetcode Java Pascal's Triangle II"
excerpt: "Leetcode Pascal's Triangle II Java 풀이"
last_modified_at: 2021-08-09T13:00:00
header:
  image: /assets/images/leetcode/pascals-triangle-ii.png
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
[Link](https://leetcode.com/pascals-triangle-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> getRow(int rowIndex) {
    List<Integer> list = new ArrayList<>();
    long num = 1;
    for (int idx = 0; idx <= rowIndex; idx++) {
      list.add((int)num);
      num = num * (rowIndex - idx) / (idx + 1);
    }
    return list;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/535581977/){:target="_blank"}

# 설명
1. 기존 [Pascal's Triangle](../pascals-triangle)와 동일하게 [파스칼의 삼각형](https://ko.wikipedia.org/wiki/%ED%8C%8C%EC%8A%A4%EC%B9%BC%EC%9D%98_%EC%82%BC%EA%B0%81%ED%98%95){:target="_blank"}에 대한 문제이다.
- 단, 파스칼의 삼각형에서 주어진 정수 rowIndex번째 행만 만드는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- 파스칼의 rowIndex번째 행의 값들을 넣을 list를 생성한다.
- 파스칼의 삼각형의 값들을 계산하기 위한 지역 변수인 num을 long형으로 정의한다.
  - long형으로 정의하는 이유는 아래의 이후 값을 계산하는 로직에서 Overflow가 발생 할 수 있기 때문이다.
- 0부터 rowIndex까지 반복하여 파스칼의 삼각형 rowIndex번째 행을 만들어준다.
  - list에 int형으로 변환한 num 값을 넣어준다.
  - num은 $num \times \frac{rowIndex - idx}{idx + 1}$ 값으로 넣어준다.

3. 반복문이 완료되면 파스칼의 삼각형을 저장한 list를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PascalsTriangle.java){:target="_blank"}에서 확인 가능합니다.