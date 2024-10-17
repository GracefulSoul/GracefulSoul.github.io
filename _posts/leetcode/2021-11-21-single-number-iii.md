---
title: "Leetcode Java Single Number III"
excerpt: "Leetcode - 'Single Number III' 문제 Java 풀이"
last_modified_at: 2021-11-21T10:00:00
header:
  image: /assets/images/leetcode/single-number-iii.png
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
[Link](https://leetcode.com/problems/single-number-iii/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] singleNumber(int[] nums) {
    int bit = 0;
    for (int num : nums) {
      bit ^= num;
    }
    int diff = bit & -bit;
    int single = 0;
    for (int num : nums) {
      if ((diff & num) != 0) {
        single ^= num;
      }
    }
    return new int[] { single, bit ^ single };
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/590226962/){:target="_blank"}

# 설명
1. 주어진 배열 nums를 이용하여 한 번만 포함된 두 숫자를 찾는 문제이다.

2. 한 번만 포함된 숫자를 저장하기 위한 변수 bit를 정의하고 0으로 초기화한다.

3. nums를 반복하여 모든 숫자에 XOR(^) 비트 연산자를 이용하여 두 번 발생하는 숫자를 무시하고 단일 발생하는 숫자들만 bit에 해당 연산자의 결과로 넣어준다.

4. bit와 -bit를 이용하여 AND(&) 비트 연산자 결과인 마지막 세트 비트를 diff에 넣어준다.

5. 단일 발생한 임의 값을 저장하기 위하여 single 변수를 정의하고 0으로 초기화한다.

6. nums를 반복하여 모든 숫자를 탐색하여 단일 발생한 값을 single에 넣어준다.
- diff와 num의 AND(&) 비트 연산 결과가 0이 아닌 경우, single과 num 값의 XOR(^) 비트 연산 결과를 single에 넣어준다.

7. bit와 single의 XOR(^) 비트 연산 결과로 단일 발생한 두 번째 값을 찾아 해당 값과, single의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SingleNumberIII.java){:target="_blank"}에서 확인 가능합니다.