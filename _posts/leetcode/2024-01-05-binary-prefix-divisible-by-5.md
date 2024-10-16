---
title: "Leetcode Java Binary Prefix Divisible By 5"
excerpt: "Leetcode Binary Prefix Divisible By 5 Java"
last_modified_at: 2024-01-05T12:30:00
header:
  image: /assets/images/leetcode/binary-prefix-divisible-by-5.png
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
[Link](https://leetcode.com/problems/binary-prefix-divisible-by-5){:target="_blank"}

# 코드
```java
class Solution {

  public List<Boolean> prefixesDivBy5(int[] nums) {
    List<Boolean> result = new ArrayList<>();
    int remainder = 0;
    for (int num : nums) {
      remainder = ((remainder << 1) + num) % 5;
      result.add(remainder == 0);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/binary-prefix-divisible-by-5/submissions/1137232572/){:target="_blank"}

# 설명
1. nums의 각 자리 순서까지 이진 표현법으로 변환할 경우, 5로 나눌 수 있는지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과를 저장할 변수로, ArrayList로 초기화한다.
- remainder는 nums의 현재 위치까지 이진 표현법의 값이 5로 나눌 수 있는지 검증하기 위해 나머지를 저장한 변수로, 0으로 초기화한다.

3. nums의 각 값을 num에 넣고 아래를 반복한다.
- remainder에 remainder의 비트를 좌측으로 한 자리 이동시킨 값에 num을 더한 후 5로 나눈 나머지를 넣어주고, 해당 값이 0인지 검증한 결과를 result에 넣어준다.

4. 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryPrefixDivisibleBy5.java){:target="_blank"}에서 확인 가능합니다.