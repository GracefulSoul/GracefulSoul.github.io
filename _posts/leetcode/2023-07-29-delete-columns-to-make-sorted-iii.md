---
title: "Leetcode Java Delete Columns to Make Sorted III"
excerpt: "Leetcode Delete Columns to Make Sorted III Java"
last_modified_at: 2023-07-29T10:00:00
header:
  image: /assets/images/leetcode/delete-columns-to-make-sorted-iii.png
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
[Link](https://leetcode.com/problems/delete-columns-to-make-sorted-iii){:target="_blank"}

# 코드
```java
class Solution {

  public int minDeletionSize(String[] strs) {
    int max = 1;
    int length = strs[0].length();
    int[] dp = new int[length];
    for (int i = 0; i < length; i++) {
      dp[i] = 1;
      for (int j = 0; j < i; j++) {
        if (this.isLexicographicOrder(strs, i, j)) {
          dp[i] = Math.max(dp[i], dp[j] + 1);
        }
      }
      max = Math.max(max, dp[i]);
    }
    return length - max;
  }

  private boolean isLexicographicOrder(String[] strs, int i, int j) {
    for (String str : strs) {
      if (str.charAt(i) < str.charAt(j)) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/delete-columns-to-make-sorted-iii/submissions/1006535820/){:target="_blank"}

# 설명
1. 동일한 길이의 문자열이 들어있는 strs의 문자열들이 사전적 순서로 정렬된 최대 길이의 문자열이 되기 위해서 동일한 위치의 문자를 삭제할 때, 최소 삭제 횟수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- max는 문자열의 최대 길이를 저장할 변수로, 1로 초기화한다.
- length는 문자열의 길이를 저장할 변수로, strs의 첫 문자열의 길이를 넣어준다.
- dp는 문자열 최대 길이를 저장하기 위한 변수로, length 길이의 정수 배열로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 수행한다.
- dp의 i번째 위치에 1을 넣어준다.
- 0부터 i미만까지 j를 증가시키며 아래를 수행한다.
  - 4번에서 정의한 isLexicographicOrder(String[] strs, int i, int j) 메서드를 수행하여 사전적 순서가 되는 경우, dp의 i번째 위치에 dp[i]와 $dp[j] + 1$ 중 큰 값을 넣어준다.
- max에 max와 dp[i]의 값 중 큰 값을 넣어 저장한다.

4. sts의 모든 문자열들의 i번째 문자와 j번째 문자가 사전적 순서인지 검증하기 위한 isLexicographicOrder(String[] strs, int i, int j) 메서드를 정의한다.
- sts의 모든 문자열의 i번째 문자가 j번째 문자보다 작은 경우, false를 모두 수행되는 경우 true를 반환한다.

5. 반복이 완료되면 length에서 문자열의 최대 길이인 max를 뺀 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DeleteColumnsToMakeSortedIII.java){:target="_blank"}에서 확인 가능합니다.