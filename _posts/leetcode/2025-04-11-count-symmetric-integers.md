---
title: "Leetcode Java Count Symmetric Integers"
excerpt: "Leetcode - 'Count Symmetric Integers' 문제 Java 풀이"
last_modified_at: 2025-04-11T21:45:00
header:
  image: /assets/images/leetcode/count-symmetric-integers.png
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
[Link](https://leetcode.com/problems/count-symmetric-integers/){:target="_blank"}

# 코드
```java
class Solution {

  public int countSymmetricIntegers(int low, int high) {
    int result = 0;
    for (int i = low; i <= high; i++) {
      String s = Integer.toString(i);
      int length = s.length();
      if (length % 2 != 0) {
        continue;
      }
      int diff = 0;
      for (int j = 0; j < length / 2; j++) {
        diff += s.charAt(j) - s.charAt(length - j - 1);
      }
      if (diff == 0) {
        result++;
      }
    }
    return result;
  }


}
```

# 결과
[Link](https://leetcode.com/problems/count-symmetric-integers/submissions/1603633988/){:target="_blank"}

# 설명
1. [low, high] 범위 내 짝수 값들 중 앞 숫자 합과 뒤 숫자 합이 동일한 숫자 갯수를 계산하는 문제이다.

2. result는 결과를 저장할 변수로, 0으로 초기화한다.

3. low부터 high 이하까지 i를 증가시키며 아래를 반복한다.
- 계산에 필요한 변수를 정의한다.
  - s는 i를 문자열로 변환한 변수이다.
  - length는 s의 길이를 저장한 변수로, 홀수인 경우 다음 반복을 수행한다.
  - diff는 앞 숫자 합과 뒤 숫자 합의 차이를 저장할 변수로, 0으로 초기화한다.
- 0부터 $\frac{length}{2}$ 미만까지 j를 증가시키며 아래를 반복한다.
  - diff에 s의 j번째 숫자에 $length - j - 1$번째 숫자를 뺀 값을 더해준다.
- diff가 0인 앞 숫자 합과 뒤 숫자 합이 동일한 조건을 만족하는 경우, result를 증가시켜준다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountSymmetricIntegers.java){:target="_blank"}에서 확인 가능합니다.