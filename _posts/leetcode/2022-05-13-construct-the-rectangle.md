---
title: "Leetcode Java Construct the Rectangle"
excerpt: "Leetcode - 'Construct the Rectangle' 문제 Java 풀이"
last_modified_at: 2022-05-13T09:00:00
header:
  image: /assets/images/leetcode/construct-the-rectangle.png
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
[Link](https://leetcode.com/problems/construct-the-rectangle/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] constructRectangle(int area) {
    int width = (int) Math.sqrt(area);
    while (area % width > 0) {
      width--;
    }
    return new int[] { area / width, width };
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/698359121/){:target="_blank"}

# 설명
1. 사각형의 면적이 area인 사각형의 길이 L과 너비 W를 배열인 [L, W] 형태로 반환하는 문제이다.
- 너비 W는 길이 L보다 크지않아야 한다.
- 길이 L과 너비 W의 차이는 가능한 작아야 한다.

2. width에 area의 제곱근의 결과를 넣어준다.
- 사각형의 면적은 $L \times W$이므로, 면적의 제곱근이 제곱수인 경우 정사각형이며 그렇지 않으면 직사각형으로 구성이 된다.

3. area를 width로 나눈 나머지가 0이 될 때까지, width를 감소시킨다.

4. 3번을 통해 구해진 width를 이용하여 area를 width로 나눈 length와 width를 정수 배열로 만들어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConstructTheRectangle.java){:target="_blank"}에서 확인 가능합니다.