---
title: "Leetcode Java House Robber IV"
excerpt: "Leetcode - 'House Robber IV' 문제 Java 풀이"
last_modified_at: 2025-03-17T17:50:00
header:
  image: /assets/images/leetcode/divide-array-into-equal-pairs.png
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
[Link](https://leetcode.com/problems/divide-array-into-equal-pairs/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean divideArray(int[] nums) {
    int[] counts = new int[501];
    for (int num : nums) {
      counts[num]++;
    }
    for (int count : counts) {
      if (count % 2 != 0) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/divide-array-into-equal-pairs/submissions/1576563375/){:target="_blank"}

# 설명
1. 짝수로 구성된 nums의 동일 숫자들을 짝으로 매칭시킬 수 있는지 검증하는 문제이다.

2. counts는 nums 내 값들의 갯수를 저장할 변수로, nums의 값들을 반복하여 갯수를 넣어준다.

3. counts의 각 값들을 순차적으로 반복하여 홀수개 존재하는 경우, 짝으로 매칭되는 값이 존재하므로 false를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 모든 값들이 짝으로 매칭될 수 있으므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DivideArrayIntoEqualPairs.java){:target="_blank"}에서 확인 가능합니다.