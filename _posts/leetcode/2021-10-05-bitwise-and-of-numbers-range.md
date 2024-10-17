---
title: "Leetcode Java Bitwise AND of Numbers Range"
excerpt: "Leetcode - 'Bitwise AND of Numbers Range' 문제 Java 풀이"
last_modified_at: 2021-10-05T13:00:00
header:
  image: /assets/images/leetcode/bitwise-and-of-numbers-range.png
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
[Link](https://leetcode.com/problems/bitwise-and-of-numbers-range/){:target="_blank"}

# 코드
```java
public class Solution {

  public int rangeBitwiseAnd(int left, int right) {
    int count = 0;
    while (left != right) {
      left >>= 1;
      right >>= 1;
      count++;
    }
    return left << count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/566009758/){:target="_blank"}

# 설명
1. 주어진 정수 left와 right의 binary code 중 공통된 접두사를 찾아 해당 값을 반환하는 문제이다.

2. 공통된 접두사를 찾기 위해 이동한 횟수를 저장할 변수인 count를 정의하고 0으로 초기화 한다.

3. left와 right가 동일한 값이 되기 전까지 두 값의 bit를 한 칸 오른쪽으로 이동시키고, count를 증가시킨다.
- left와 right의 bit를 우측으로 계속 이동하다 동일한 값이 되는 구간이 두 값의 공통된 접두사가 되는 지점이다.

4. 공통된 접두사가 저장된 left에 우측으로 이동한 횟수인 count만큼 좌측으로 이동시켜 해당 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BitwiseANDOfNumbersRange.java){:target="_blank"}에서 확인 가능합니다.