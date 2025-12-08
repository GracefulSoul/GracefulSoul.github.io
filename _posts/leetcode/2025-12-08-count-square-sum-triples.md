---
title: "Leetcode Java Count Square Sum Triples"
excerpt: "Leetcode - 'Count Square Sum Triples' 문제 Java 풀이"
last_modified_at: 2025-12-08T18:30:00
header:
  image: /assets/images/leetcode/count-square-sum-triples.png
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
[Link](https://leetcode.com/problems/count-square-sum-triples/){:target="_blank"}

# 코드
```java
class Solution {

  public int countTriples(int n) {
    int result = 0;
    for (int i = 3; i < n - 1; i++) {
      for (int j = i + 1; j < n; j++) {
        int volume = (i * i) + (j * j);
        int sqrt = (int) Math.sqrt(volume);
        if (sqrt * sqrt == volume && sqrt <= n) {
          result += 2;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-square-sum-triples/submissions/1850006448/){:target="_blank"}

# 설명
1. n 이하의 임의 세 값을 이용해서 만들 수 있는 직삼각형의 갯수를 계산하는 문제이다.

2. result는 만들 수 있는 직삼각형의 갯수를 저장할 변수로, 0으로 초기화한다.

3. i는 3부터 $n - 1$ 미만까지 1씩 증가시키고, j는 $i + 1$부터 n 미만까지 1씩 증가시키며 아래를 반복한다.
- 사각형의 부피인 volume을 $(i \times i) + (j \times j)$ 값으로 초기화한다.
- 대각선의 길이인 sqrt에 volume 제곱근 값을 정수형으로 넣어준다.
- $sqrt \times sqrt$의 값이 volume이면서 sqrt의 값이 n 이하인 조건을 만족하는 직사각형을 만들 수 있는 경우, x축과 y축이 긴 경우의 두 경우를 result에 더해준다.

4. 조건을 만족하는 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountSquareSumTriples.java){:target="_blank"}에서 확인 가능합니다.