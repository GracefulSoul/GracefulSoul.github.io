---
title: "Leetcode Java Special Array With X Elements Greater Than or Equal X"
excerpt: "Leetcode Easy - 'Special Array With X Elements Greater Than or Equal X' 문제 Java 풀이"
last_modified_at: 2024-05-27T18:40:00
header:
  image: /assets/images/leetcode/special-array-with-x-elements-greater-than-or-equal-x.png
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
[Link](https://leetcode.com/problems/special-array-with-x-elements-greater-than-or-equal-x/){:target="_blank"}

# 코드
```java
class Solution {

  public int specialArray(int[] nums) {
    int length = nums.length;
    int[] counts = new int[length + 1];
    for (int num : nums) {
      if (num >= length) {
        counts[length]++;
      } else {
        counts[num]++;
      }
    }
    int result = 0;
    for (int i = length; i > 0; i--) {
      result += counts[i];
      if (result == i) {
        return i;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/special-array-with-x-elements-greater-than-or-equal-x/submissions/1269264215/){:target="_blank"}

# 설명
1. nums의 값들보다 크거나 같은 숫자들이 x개 존재하는 숫자 x를 찾는 문제이다.
- 단, x가 존재하지 않으면 -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- counts는 nums의 숫자 갯수를 저장할 변수로, nums의 num에 순차적으로 값을 넣어 num이 length 보다 크거나 같으면 counts[length]를 아니면 마지막 값인 counts[num]을 증가시켜준다.
- result는 x를 찾기위한 변수로 변수로, 0으로 초기화한다.

3. length부터 0 초과일 때 까지 i를 감소시키며 아래를 반복한다.
- result에 counts[i]의 값을 더해주고, result와 i가 동일한 x가 성립되면 해당 값을 반환한다.

4. 반복이 완료되면 x가 존재하지 않으므로, -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SpecialArrayWithXElementsGreaterThanOrEqualX.java){:target="_blank"}에서 확인 가능합니다.