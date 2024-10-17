---
title: "Leetcode Java Minimum Number of Operations to Make Array Empty"
excerpt: "Leetcode Medium - 'Minimum Number of Operations to Make Array Empty' 문제 Java 풀이"
last_modified_at: 2024-01-04T12:10:00
header:
  image: /assets/images/leetcode/minimum-number-of-operations-to-make-array-empty.png
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
[Link](https://leetcode.com/problems/minimum-number-of-operations-to-make-array-empty){:target="_blank"}

# 코드
```java
class Solution {

  public int minOperations(int[] nums) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int num : nums) {
      map.put(num, map.getOrDefault(num, 0) + 1);
    }
    int result = 0;
    for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
      int value = entry.getValue();
      if (value == 1) {
        return -1;
      }
      result += value / 3;
      if (value % 3 != 0) {
        result++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-number-of-operations-to-make-array-empty/submissions/1136206658/){:target="_blank"}

# 설명
1. nums내 동일한 값을 둘, 셋 단위로 제거할 때 모두 제거하기까지 걸리는 최소한의 작업 수를 반환하는 문제이다.
- 단, 삭제가 불가능한 경우 -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 숫자별 갯수를 계산하기 위한 변수로, HashMap으로 정의하고 nums 내 숫자 별 갯수를 모두 넣어준다.
- result는 횟수를 계산하기 위한 변수로, 0으로 초기화한다.

3. map의 각 값을 entry에 넣고 아래를 반복한다.
- value에 entry의 값을 넣어주고, 1인 경우 잔여 값이 되므로 -1을 주어진 문제의 결과로 반환한다.
- result에 value가 3배수이면 3으로 나눈 값을, 아니면 3으로 나눈 값에 1을 증가한 값을 더해준다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumNumberOfOperationsToMakeArrayEmpty.java){:target="_blank"}에서 확인 가능합니다.