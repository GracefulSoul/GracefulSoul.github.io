---
title: "Leetcode Java Minimum Increment to Make Array Unique"
excerpt: "Leetcode Medium - 'Minimum Increment to Make Array Unique' 문제 Java 풀이"
last_modified_at: 2023-07-12T19:30:00
header:
  image: /assets/images/leetcode/minimum-increment-to-make-array-unique.png
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
[Link](https://leetcode.com/problems/minimum-increment-to-make-array-unique){:target="_blank"}

# 코드
```java
class Solution {

  public int minIncrementForUnique(int[] nums) {
    Arrays.sort(nums);
    int result = 0;
    int need = 0;
    for (int num : nums) {
      result += Math.max(need - num, 0);
      need = Math.max(num, need) + 1;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-increment-to-make-array-unique/submissions/992570052/){:target="_blank"}

# 설명
1. nums의 값이 모두 고유한 값이 되기 위하여 변경하는 값의 합을 구하는 문제이다.

2. nums를 오름차순으로 정렬한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- result는 변경하는 값의 합을 저장할 변수로, 0으로 초기화한다.
- need는 다음에 필요한 값을 저장할 변수로, 0으로 초기화한다.

4. nums의 모든 값을 num에 순차적으로 넣고 아래를 반복한다.
- result에 $need - num$의 값과 0 중 큰 값인 차이 값을 넣어준다.
- need는 num과 need 중 큰 값보다 1 큰 숫자를 넣어준다.

5. 반복이 완료되면 값의 차이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumIncrementToMakeArrayUnique.java){:target="_blank"}에서 확인 가능합니다.