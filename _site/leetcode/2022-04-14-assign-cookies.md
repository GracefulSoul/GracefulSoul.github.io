---
title: "Leetcode Java Assign Cookies"
excerpt: "Leetcode Assign Cookies Java 풀이"
last_modified_at: 2022-04-14T13:00:00
header:
  image: /assets/images/leetcode/assign-cookies.png
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
[Link](https://leetcode.com/problems/assign-cookies/){:target="_blank"}

# 코드
```java
class Solution {

  public int findContentChildren(int[] g, int[] s) {
    Arrays.sort(g);
    Arrays.sort(s);
    int i = 0;
    for (int j = 0; i < g.length && j < s.length; j++) {
      if (g[i] <= s[j]) {
        i++;
      }
    }
    return i;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/679974327/){:target="_blank"}

# 설명
1. 아이들이 만족할 쿠키의 최소 크기인 g 배열과 각 크기 별 쿠키를 담은 j 배열을 이용하여 만족한 아이의 수를 구하는 문제이다.

2. 주어진 정수 배열 g와 s를 오름차순으로 정렬한다.

3. g 배열을 탐색할 인덱스인 i를 0으로 초기화 하여 정의하고, 0부터 i가 g의 길이 미만이고 j가 s의 길이 미만일 때 까지 j를 증가시키며 반복을 수행한다.
- g의 i번째 값이 s의 j번째 값보다 작거나 같으면 i를 증가시키고, 반복을 계속 수행한다.

4. 반복이 완료되면 만족할 쿠키를 받은 아이들의 수를 저장한 i를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AssignCookies.java){:target="_blank"}에서 확인 가능합니다.