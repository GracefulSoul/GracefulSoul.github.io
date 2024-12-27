---
title: "Leetcode Java Count Vowels Permutation"
excerpt: "Leetcode - 'Count Vowels Permutation' 문제 Java 풀이"
last_modified_at: 2024-12-27T15:30:00
header:
  image: /assets/images/leetcode/count-vowels-permutation.png
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
[Link](https://leetcode.com/problems/count-vowels-permutation/){:target="_blank"}

# 코드
```java
class Solution {

  private static final int MOD = 1000000007;

  public int countVowelPermutation(int n) {
    long a = 1;
    long e = 1;
    long i = 1;
    long o = 1;
    long u = 1;
    for (int j = 1; j < n; j++) {
      long nextA = e;
      long nextE = (a + i) % MOD;
      long nextI = (a + e + o + u) % MOD;
      long nextO = (i + u) % MOD;
      long nextU = a;
      a = nextA;
      e = nextE;
      i = nextI;
      o = nextO;
      u = nextU;
    }
    return (int) ((a + e + i + o + u) % MOD);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-vowels-permutation/submissions/1489504737/){:target="_blank"}

# 설명
1. n 길이로 아래 규칙을 만족하게 만들 수 있는 문자열 갯수를 구하는 문제이다.
- 단, 값이 매울 클 수 있으므로 모듈러 $10^9 + 7$을 적용한다.
- 문자열은 소문자 'a', 'e', 'i', 'o', 'u'으로 구성된다.
- 'a' 문자 뒤에는 'e' 문자만 이어 붙일 수 있다.
- 'e' 문자 뒤에는 'a' 문자 또는 'i' 문자만 이어 붙일 수 있다.
- 'i' 문자 뒤에는 'i' 문자를 이어 붙일 수 없다.
- 'o' 문자 뒤에는 'i' 문자 또는 'u' 문자만 이어 붙일 수 있다.
- 'u' 문자 뒤에는 'a' 문자만 이어 붙일 수 있다.

2. MOD는 모듈러 $10^9 + 7$ 값을 저장한다.

3. a, e, i, o, u는 각 문자의 갯수를 계산하기 위한 변수로, 값이 int보다 클 수 있으므로 long 타입으로 정의 후 1로 초기화한다.

4. 1부터 n 미만까지 j를 증가시키며 아래를 반복한다.
- nextA는 a로 시작하는 문자 갯수를 계산할 변수로, 다음에 올 수 있는 문자인 e의 갯수를 넣어준다.
- nextE는 e로 시작하는 문자 갯수를 계산할 변수로, 다음에 올 수 있는 문자인 a와 i의 갯수를 더해 MOD로 나눈 값을 넣어준다.
- nextI는 i로 시작하는 문자 갯수를 계산할 변수로, 다음에 올 수 없는 문자인 i를 제외한 모든 값을 더해 MOD로 나눈 값을 넣어준다.
- nextO는 o로 시작하는 문자 갯수를 계산할 변수로, 다음에 올 수 있는 문자인 i와 u의 갯수를 더해 MOD로 나눈 값을 넣어준다.
- nextU는 u로 시작하는 문자 갯수를 계산할 변수로, 다음에 올 수 있는 문자인 a의 갯수를 넣어준다.
- a, e, i, o, u에 현재까지 가능한 다음 문자 길이인 nextA, nextE, nextI, nextO, nextU를 넣어준다.

5. 반복이 완료되면 a, e, i, o, u를 더한 값을 MOD로 나눈 후 int형으로 바꿔 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountVowelsPermutation.java){:target="_blank"}에서 확인 가능합니다.