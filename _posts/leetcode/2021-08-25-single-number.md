---
title: "Leetcode Java Single Number"
excerpt: "Leetcode - 'Single Number' 문제 Java 풀이"
last_modified_at: 2021-08-25T13:00:00
header:
  image: /assets/images/leetcode/single-number.png
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
[Link](https://leetcode.com/problems/single-number/){:target="_blank"}

# 코드
```java
class Solution {

  public int singleNumber(int[] nums) {
    int result = 0;
    for (int num : nums) {
      result ^= num;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/543789135/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums에서 하나만 포함된 숫자를 탐색하는 문제이다.

2. 결과를 저장할 정수 result를 정의한다.

3. 반복문을 통해 배타적 논리합(XOR)를 수행하여 결과를 result에 넣어준다.
- 배타적 논리합은 짝수번 수행할 경우, 0이 되므로 홀수번 수행한 결과만 남게 된다.
- 2개씩 들어간 숫자들은 위의 경우로 0이 되고, 1개만 들어가 있는 목표 숫자만 남는 것이다.

4. 하나만 포함된 숫자를 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SingleNumber.java){:target="_blank"}에서 확인 가능합니다.