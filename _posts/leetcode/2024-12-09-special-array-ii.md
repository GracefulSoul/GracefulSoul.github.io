---
title: "Leetcode Java Special Array II"
excerpt: "Leetcode - 'Special Array II' 문제 Java 풀이"
last_modified_at: 2024-12-08T12:20:00
header:
  image: /assets/images/leetcode/special-array-ii.png
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
[Link](https://leetcode.com/problems/special-array-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean[] isArraySpecial(int[] nums, int[][] queries) {
    boolean[] result = new boolean[queries.length];
    int[] counts = new int[nums.length];
    for (int i = 1; i < nums.length; i++) {
      counts[i] = counts[i - 1];
      if (nums[i - 1] % 2 == nums[i] % 2) {
        counts[i]++;
      }
    }
    for (int i = 0; i < queries.length; i++) {
      int[] query = queries[i];
      result[i] = counts[query[1]] - counts[query[0]] == 0;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/special-array-ii/submissions/1474195828/){:target="_blank"}

# 설명
1. nums내 queries의 각 구간 별 숫자들이 홀수와 짝수가 번갈아 나오는지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과를 저장할 변수로, queries 길이의 boolean 배열로 초기화한다.
- counts는 nums 내 연속된 짝수 갯수를 저장할 변수로, nums 길이의 정수 배열로 초기화한다.

3. 1부터 nums 길이 미만까지 i를 증가시키며 아래를 반복한다.
- counts[i]에 이전까지 갯수인 counts[$i - 1$]의 값을 넣어준다.
- nums[$i - 1$]과 nums[i]가 짝수인 경우, count[i]를 증가시켜준다.

4. 0부터 queries의 길이 미만까지 i를 증가시키면서 아래를 반복한다.
- query에 queries[i]의 값을 넣어준다.
- result[i]의 위치에 $counts[query[1]] - counts[query[0]]$의 값이 0인 연속으로 짝수가 존재하는 구간이 유지되는지 여부를 넣어준다.

5. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SpecialArrayII.java){:target="_blank"}에서 확인 가능합니다.