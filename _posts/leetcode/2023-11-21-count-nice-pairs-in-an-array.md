---
title: "Leetcode Java Count Nice Pairs in an Array"
excerpt: "Leetcode Medium - 'Count Nice Pairs in an Array' 문제 Java 풀이"
last_modified_at: 2023-11-21T18:50:00
header:
  image: /assets/images/leetcode/count-nice-pairs-in-an-array.png
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
[Link](https://leetcode.com/problems/count-nice-pairs-in-an-array){:target="_blank"}

# 코드
```java
class Solution {

  public int countNicePairs(int[] nums) {
    int result = 0;
    Map<Integer, Integer> map = new HashMap<>();
    for (int num : nums) {
      int reverse = 0;
      for (int i = num; i > 0; i /= 10) {
        reverse = (reverse * 10) + (i % 10);
      }
      int value = map.getOrDefault(num - reverse, 0);
      map.put(num - reverse, value + 1);
      result = (result + value) % 1000000007;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-nice-pairs-in-an-array/submissions/1103351421/){:target="_blank"}

# 설명
1. nums 내 두 값 중 한 값만 반전시켜 번갈아 더한 값이 동일한 쌍의 수를 구하는 문제이다.
- 단, 쌍의 수가 매우 클 수 있으므로 모듈러 $10^9 + 7$을 적용한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 쌍의 수를 저장할 변수로, 0으로 초기화한다.
- map은 쌍의 수를 계산하기위한 변수로, HashMap으로 초기화한다.

3. nums의 모든 값을 num에 순차적으로 넣어 아래를 반복한다.
- reverse에 num의 값을 반전시켜 넣어준다.
- value에 map 내 $num - reverse$의 결과가 키인 값인 동일한 쌍의 수가 있으면 해당 값을 꺼내고, 아니면 0으로 초기화한다.
- map에 $num - reverse$가 키인 값에 $value + 1$을 넣어준다.
- result에 $result + value$를 모듈러 $10^9 + 7$을 적용한 값을 넣어준다.
  
4. 반복이 완료되면 모듈러를 적용한 쌍의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 해설
- 두 값 중 한 값만 반전시켜 번갈아 더한 값이 동일한 경우, 자기 자신의 값에 반전시킨 값을 뺀 결과가 동일한다.
- 예를 들어, 42와 97의 경우 $42 + 79 = 24 + 97 = 121$를 만족하며 $42 - 24 = 97 - 79 = 18$을 만족한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountNicePairsInAnArray.java){:target="_blank"}에서 확인 가능합니다.