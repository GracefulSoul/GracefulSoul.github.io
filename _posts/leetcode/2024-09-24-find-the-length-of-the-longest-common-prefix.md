---
title: "Leetcode Java Find the Length of the Longest Common Prefix"
excerpt: "Leetcode Find the Length of the Longest Common Prefix Java"
last_modified_at: 2024-09-24T18:40:00
header:
  image: /assets/images/leetcode/find-the-length-of-the-longest-common-prefix.png
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
[Link](https://leetcode.com/problems/find-the-length-of-the-longest-common-prefix/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestCommonPrefix(int[] arr1, int[] arr2) {
    Set<Integer> set = new HashSet<>();
    for (int num : arr1) {
      while (!set.contains(num) && num > 0) {
        set.add(num);
        num /= 10;
      }
    }
    int result = 0;
    for (int num : arr2) {
      while (!set.contains(num) && num > 0) {
        num /= 10;
      }
      if (num > 0) {
        result = Math.max(result, (int) Math.log10(num) + 1);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-length-of-the-longest-common-prefix/submissions/1400542081/){:target="_blank"}

# 설명
1. arr1과 arr2의 값들 중 가장 긴 접두 문자의 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- set은 각 가능한 숫자들을 넣어줄 변수로, 중복을 배제하기 위해서 HashSet로 초기화 후 아래를 수행한다.
  - arr1의 값들을 순차적으로 num에 넣어 set에 num이 존재하지 않으면서 num이 0 초과일 때까지, set에 num을 넣고 num에 자기 자신을 10으로 나눈 몫을 넣어준다.
- result는 가장 긴 접두 문자의 길이를 저장하기 위한 변수로, 0으로 초기화한다.

3. arr2의 값을 순차적으로 num에 넣어 아래를 수행한다.
- set에 num이 존재하지 않으면서 num이 0 초과일 때까지, num에 10을 나눈 값을 넣어준다.
- num이 0 초과인 접두사가 가능한 길이인 경우, result에 result와 num을 log10한 결과에 1을 더한 길이 중 큰 값을 넣어준다.

4. 반복이 완료되면 가장 긴 접두 문자의 길이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CriticalConnectionsInANetwork.java){:target="_blank"}에서 확인 가능합니다.