---
title: "Leetcode Java Alternating Groups II"
excerpt: "Leetcode - 'Alternating Groups II' 문제 Java 풀이"
last_modified_at: 2025-03-09T19:55:00
header:
  image: /assets/images/leetcode/alternating-groups-ii.png
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
[Link](https://leetcode.com/problems/alternating-groups-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int numberOfAlternatingGroups(int[] colors, int k) {
    int length = colors.length;
    int result = 0;
    int i = 0;
    for (int j = 0; j < length + k - 1; j++) {
      if (0 < j && colors[j % length] == colors[(j - 1) % length]) {
        i = j;
      }
      if (k <= j - i + 1) {
        result++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/alternating-groups-ii/submissions/1567974645/){:target="_blank"}

# 설명
1. 아래 규칙대로 구성된 정수 배열인 colors에서 k개의 인접한 색깔이 번갈아 나타난 횟수를 계산하는 문제이다.
- 0은 빨간색 타일을, 1은 파란색 타일을 의미한다.
- colors의 값들을 원형으로 이어주므로, 첫 값과 마지막 값은 인접한 상태이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 colors의 길이를 저장한 변수이다.
- result는 결과 갯수를 계산하기 위한 변수로, 0으로 초기화한다.
- i는 인접한 색깔이 번갈아 나타나기 시작한 위치 값을 저장할 변수로, 0으로 초기화한다.

3. 0부터 $length + k - 1$ 미만까지 j를 증가시키며 아래를 반복한다.
- j가 0 초과이면서 colors 내 j를 length로 나눈 값의 나머지 위치의 값과 $j - 1$을 length로 나눈 값의 나머지 위치의 값이 동일한 경우, i에 j를 넣어 시작 위치를 이동한다.
- k가 $j - i + 1$보다 작거나 같은 조건에 부합하는 경우, result를 증가시켜 갯수를 계산해준다.

4. 반복이 완료되면 조건에 부합한 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AlternatingGroupsII.java){:target="_blank"}에서 확인 가능합니다.