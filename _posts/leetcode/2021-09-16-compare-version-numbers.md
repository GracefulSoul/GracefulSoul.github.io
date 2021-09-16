---
title: "Leetcode Java Compare Version Numbers"
excerpt: "Leetcode Compare Version Numbers Java 풀이"
last_modified_at: 2021-09-16T12:00:00
header:
  image: /assets/images/leetcode/compare-version-numbers.png
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
[Link](https://leetcode.com/problems/compare-version-numbers/){:target="_blank"}

# 코드
```java
class Solution {

  public int compareVersion(String version1, String version2) {
    String[] splitVersion1 = version1.split("\\.");
    String[] splitVersion2 = version2.split("\\.");
    for (int idx = 0; idx < splitVersion1.length || idx < splitVersion2.length; idx++) {
      int int1 = idx < splitVersion1.length ? Integer.parseInt(splitVersion1[idx]) : 0;
      int int2 = idx < splitVersion2.length ? Integer.parseInt(splitVersion2[idx]) : 0;
      if (int1 > int2) {
        return 1;
      } else if (int1 < int2) {
        return -1;
      }
    }
    return 0;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/555661062/){:target="_blank"}

# 설명
1. 주어진 문자열 version1과 version2은 숫자열과 점(.) 만 포함된 버전 표기법으로, 어느 문자열의 버전이 더 높은지에 따라 결과를 반환하는 문제이다.
- version1의 버전이 높으면 1을, version2의 버전이 높으면 -1을, 동일하면 0을 주어진 문제의 결과로 반환한다.

2. version1과 version2를 점(.)을 구분자로 배열로 변경하여 각자 splitVersion1, splitVersion2에 넣어준다.

3. splitVersion1과 splitVersion2 중 가장 값이 많이 들어가 있는 배열 기준으로 반복을 수행하여 높은 버전을 확인한다.
- 각 버전 중 하위 버전 값이 없을(배열의 크기가 더 작은) 경우, 0으로 비교를 수행한다.
- version1의 부분 버전(splitVersion1의 idx번째 숫자) 값이 높을 경우, 1을 주어진 문제의 결과로 반환한다.
- version2의 부분 버전(splitVersion2의 idx번째 숫자) 값이 높을 경우, -1을 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 동일한 버전이므로, 0을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CompareVersionNumbers.java){:target="_blank"}에서 확인 가능합니다.