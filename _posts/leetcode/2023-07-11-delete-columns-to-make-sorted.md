---
title: "Leetcode Java Delete Columns to Make Sorted"
excerpt: "Leetcode Easy - 'Delete Columns to Make Sorted' 문제 Java 풀이"
last_modified_at: 2023-07-11T18:50:00
header:
  image: /assets/images/leetcode/delete-columns-to-make-sorted.png
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
[Link](https://leetcode.com/problems/delete-columns-to-make-sorted){:target="_blank"}

# 코드
```java
class Solution {

  public int minDeletionSize(String[] strs) {
    int result = 0;
    for (int i = 0; i < strs[0].length(); i++) {
      char prev = strs[0].charAt(i);
      for (int j = 1; j < strs.length; j++) {
        char c = strs[j].charAt(i);
        if (c < prev) {
          result++;
          break;
        }
        prev = c;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximize-the-confusion-of-an-exam/submissions/988513311/){:target="_blank"}

# 설명
1. 동일한 길이의 문자열로 이루어진 strs를 이용하여 각 문자열의 동일한 위치의 문자들을 순차적으로 묶었을 때 사전 순으로 이루어지지 않는 위치의 갯수를 구하는 문제이다.

2. result는 사전 순으로 이루어지지 않는 위치의 갯수를 계산할 변수로, 0으로 초기화한다.

3. 0부터 strs의 문자 길이 미만까지 i를 증가시키며 아래를 반복한다.
- prev는 이전 문자를 순차적으로 저장할 변수로, 첫 문자열의 i번째 문자를 넣어 초기화한다.
- 1부터 strs의 길이 미만까지 j를 증가시키며 아래를 반복한다.
  - c는 각 위치 별 문자를 저장할 변수로, strs의 j번째 문자열의 i번째 문자를 넣어준다.
  - c가 prev보다 작은 경우, result를 증가시키고 반복을 중지한다.
  - 위의 경우가 아니라면 prev에 c를 넣고 반복을 계속한다.

4. 반복이 완료되면 조건에 대한 갯수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DeleteColumnsToMakeSorted.java){:target="_blank"}에서 확인 가능합니다.