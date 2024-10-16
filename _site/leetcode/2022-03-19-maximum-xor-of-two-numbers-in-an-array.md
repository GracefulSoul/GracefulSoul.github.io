---
title: "Leetcode Java Maximum XOR of Two Numbers in an Array"
excerpt: "Leetcode Maximum XOR of Two Numbers in an Array Java 풀이"
last_modified_at: 2022-03-19T13:00:00
header:
  image: /assets/images/leetcode/maximum-xor-of-two-numbers-in-an-array.png
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
[Link](https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int findMaximumXOR(int[] nums) {
    int result = 0;
    int mask = 0;
    int max = 0;
    for (int num : nums) {
      max = Math.max(max, num);
    }
    Set<Integer> set = new HashSet<>();
    for (int idx = 31 - Integer.numberOfLeadingZeros(max); idx >= 0; idx--) {
      set.clear();
      int bit = 1 << idx;
      mask |= bit;
      int maxBit = result | bit;
      for (int num : nums) {
        int temp = num & mask;
        if (set.contains(temp ^ maxBit)) {
          result = maxBit;
          break;
        }
        set.add(temp);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/662795016/){:target="_blank"}

# 설명
1. 주어진 nums를 이용하여 nums 내 임의 두 값의 XOR 연산의 결과가 가장 큰 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 XOR 연산의 결과가 가장 큰 값을 넣을 변수로, 0으로 초기화한다.
- mask는 비트를 마스킹하기 위한 변수로, 0으로 초기화한다.
- max는 nums 배열 내 최댓값을 넣기 위한 변수로, nums 배열을 순회하여 최댓값을 넣어준다.
- set은 XOR의 최댓값이 되는 값을 구하기 위해 임시로 값을 넣을 변수로, HashSet으로 정의한다.

3. 31에서 max의 비트 값에서 맨 처음 1이 나온 위치 앞의 0의 개수를 빼준 값부터 0 이상까지 idx를 감소시키며 반복한다.
- 해당 최댓값을 이용하여 비트 연산을 수행할 결우 overflow되는 부분을 배제하고 탐색하기 위해서 해당 자릿수 만큼 제거하고 수행한다.
- set을 초기화하고, bit에 1을 좌측으로 idx번 이동시킨 값을 넣어준다.
- mask에 mask와 bit의 OR(&#124;) 비트 연산의 수행 결과를 넣어준다.
- maxBit에 result와 bit의 OR(&#124;) 비트 연산의 수행 결과를 넣어준다.
- nums를 반복하여 아래를 수행한다.
  - temp에 num과 mask의 AND(&) 비트 연산의 수행 결과를 넣어준다.
  - temp와 maxBit의 XOR(^) 비트 연산의 수행결과가 set에 존재하면, 최댓값인 maxBit를 result에 넣어 반복을 종료한다.
  - 위를 수행하고 set에 temp를 넣어주고 반복을 계속 수행한다.

4. 반복을 수행하여 nums 내 임의 두 값의 XOR 연산의 결과가 가장 큰 값을 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumXOROfTwoNumbersInAnArray.java){:target="_blank"}에서 확인 가능합니다.