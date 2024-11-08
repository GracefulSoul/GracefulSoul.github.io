---
title: "Leetcode Java Maximum XOR for Each Query"
excerpt: "Leetcode - 'Maximum XOR for Each Query' 문제 Java 풀이"
last_modified_at: 2024-11-08T18:20:00
header:
  image: /assets/images/leetcode/maximum-xor-for-each-query.png
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
[Link](https://leetcode.com/problems/maximum-xor-for-each-query/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] getMaximumXor(int[] nums, int maximumBit) {
    int length = nums.length;
    int[] result = new int[length];
    int num = (1 << maximumBit) - 1;
    for (int i = 0; i < length; i++) {
      num ^= nums[i];
      result[(length - 1) - i] = num;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-xor-for-each-query/submissions/1446595893/){:target="_blank"}

# 설명
1. nums의 각 위치 별 값부터 마지막 값까지 값들과 k까지 XOR(^) 비트 연산을 수행한 결과가 최대인 값이 되기 위한 $2^maximumBit$ 미만인 k를 각 수행 별 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- result는 결과를 반환하기 위한 변수로, length 크기의 정수 배열로 초기화한다.
- num은 각 위치 별 k를 저장할 변수로, $2^maximumBit - 1$인 값의 범위에서 1 작은 값을 넣어준다.

3. 0부터 length 미만까지 i를 증가시키면서 아래를 반복한다.
- num에 nums[i]의 값을 XOR(^) 비트 연산을 수행한다.
- result[$(length - 1) - i$]인 현재 위치에서 반대 위치의 result에 num을 넣어준다.

4. 반복이 완료되면 각 결과가 저장된 result를 주어진 문제의 결과로 반한한다.

# 해설
- n 크기의 배열 nums의 $k = nums[0] ^ nums[1] ^ ... ^ nums[n - 1] ^ k$의 결과가 최대인 결과인 $2^maximumBit - 1$이 되어야 한다는 것은, k = $2^maximumBit - 1$이 된다는 것이다.
- 위의 이야기대로 처음 위치에서는 k가 반드시 $2^maximumBit - 1$가 되어야 한다.
- 그 다음 값부터는 nums[i]의 값을 num과 XOR(^) 비트연산을 수행한 결과가 k가 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumXORForEachQuery.java){:target="_blank"}에서 확인 가능합니다.