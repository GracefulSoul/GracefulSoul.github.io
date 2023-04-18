---
title: "Leetcode Java Valid Permutations for DI Sequence"
excerpt: "Leetcode Valid Permutations for DI Sequence Java"
last_modified_at: 2023-04-18T20:30:00
header:
  image: /assets/images/leetcode/valid-permutations-for-di-sequence.png
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
[Link](https://leetcode.com/problems/valid-permutations-for-di-sequence){:target="_blank"}

# 코드
```java
class Solution {

  public int numPermsDISequence(String s) {
    int length = s.length();
    int mod = 1000000007;
    int[] dp1 = new int[length + 1];
    int[] dp2 = new int[length];
    for (int i = 0; i <= length; i++) {
      dp1[i] = 1;
    }
    for (int i = 0; i < length; i++) {
      int curr = 0;
      if (s.charAt(i) == 'I') {
        for (int j = 0; j < length - i; j++) {
          dp2[j] = curr = (curr + dp1[j]) % mod;
        }
      } else {
        for (int j = length - i - 1; j >= 0; j--) {
          dp2[j] = curr = (curr + dp1[j + 1]) % mod;
        }
      }
      dp1 = Arrays.copyOf(dp2, length);
    }
    return dp1[0];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/valid-permutations-for-di-sequence/submissions/935760424/){:target="_blank"}

# 설명
1. 아래의 규칙으로 이루어진 문자열 s를 이용하여 유효 순열의 수를 구하는 문제이다.
- 유효 순열은 [0, s.length] 범위에 있는 모든 정수의 $s.length + 1$ 정수 순열이다.
- s[i] == 'D'인 경우 값의 감소를 의미하며, 순열의 i번째 값이 $i + 1$번째 값보다 크다.
- s[i] == 'I'인 경우 값의 증가를 의미하며, 순열의 i번째 값이 $i + 1$번째 값보다 작다.
- 단, 유효 순열의 수가 매우 많을 수 있으므로, 모듈러 $10^9 + 7$를 이용하여 값을 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 s의 길이를 저장한 변수이다.
- mod는 모듈러를 적용할 변수로, $10^9 +7$로 초기화한다.
- dp1과 dp2는 유효 순열의 수를 계산하기 위한 변수로, $length + 1$크기와 length 크기의 정수 배열로 초기화하고 dp1의 모든 위치에 1을 넣어준다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 수행한다.
- curr은 현재 값을 임시 저장할 변수로, 0으로 초기화한다.
- s의 i번째 문자가 'I'인 경우, 아래를 수행한다.
  - 0부터 $length - i$까지 j를 증가시키며, dp2의 j번째 위치와 curr에 $\frac{curr + dp1[j]}{mod}$ 값을 넣어 값의 증가시켜준다.
- s의 i번째 문자가 'D'인 경우, 아래를 수행한다.
  - $length - i - 1$부터 0 이상까지 j를 감소시키며, dp2의 j번째 위치와 curr에 $\frac{curr + dp1[j + 1]}{mod}$ 값을 넣어 값을 역순으로 증가시켜준다.
- dp1에 dp2의 length 길이까지의 배열을 복사하여 넣어준다.

4. 반복이 완료되면 계산도니 유효 순열의 수인 dp1의 첫 번째 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidPermutationsForDISequence.java){:target="_blank"}에서 확인 가능합니다.