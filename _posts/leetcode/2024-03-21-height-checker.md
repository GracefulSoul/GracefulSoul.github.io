---
title: "Leetcode Java Height Checker"
excerpt: "Leetcode Easy - 'Height Checker' 문제 Java 풀이"
last_modified_at: 2024-03-21T18:55:00
header:
  image: /assets/images/leetcode/height-checker.png
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
[Link](https://leetcode.com/problems/height-checker/){:target="_blank"}

# 코드
```java
class Solution {

  public int heightChecker(int[] heights) {
    int[] counts = new int[101];
    for (int height : heights) {
      counts[height]++;
    }
    int result = 0;
    int i = 0;
    for (int height : heights) {
      while (counts[i] == 0) {
        i++;
      }
      if (i != height) {
        result++;
      }
      counts[i]--;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/height-checker/submissions/1209893525/){:target="_blank"}

# 설명
1. heights의 값들이 오름차순으로 정렬되지 않은 값의 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- counts는 heights 내 값들의 갯수를 저장할 변수로, 값의 상한인 100까지 들어갈 수 있도록 101 크기의 정수 배열로 초기화 후 heights의 값들의 갯수를 넣어준다.
- result는 정렬되지 않은 값의 갯수를 저장할 변수로, 0으로 초기화한다.
- i는 현재 높이 값을 저장할 변수로, 0으로 초기화한다.

3. heights의 모든 값들을 순차적으로 height에 넣고 아래를 반복한다.
- counts[i]의 값이 0인 heights에 존재하지 않는 값인 경우, 존재하는 위치까지 i를 계속 증가시킨다.
- i와 height가 다른 경우 현재 위치에 맞지 않는 높이이므로, result를 증가시킨다.
- 값을 차감한 count[i]의 값을 감소시킨다.

4. 반복이 완료되면 정렬되지 않은 값의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/HeightChecker.java){:target="_blank"}에서 확인 가능합니다.