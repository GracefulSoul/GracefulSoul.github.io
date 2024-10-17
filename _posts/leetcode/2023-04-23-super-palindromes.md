---
title: "Leetcode Java Super Palindromes"
excerpt: "Leetcode - 'Super Palindromes' 문제 Java 풀이"
last_modified_at: 2023-04-23T14:30:00
header:
  image: /assets/images/leetcode/super-palindromes.png
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
[Link](https://leetcode.com/problems/super-palindromes){:target="_blank"}

# 코드
```java
class Solution {

  public int superpalindromesInRange(String left, String right) {
    int result = 9 >= Long.parseLong(left) && 9 <= Long.parseLong(right) ? 1 : 0;
    for (int i = 1; i < 19684; i++) {
      String num = Integer.toString(i, 3);
      if (this.isPalindrome(num)) {
        long square = Long.parseLong(num) * Long.parseLong(num);
        if (square > Long.parseLong(right)) {
          return result;
        }
        if (square >= Long.parseLong(left) && this.isPalindrome(Long.toString(square))) {
          result++;
        }
      }
    }
    return result;
  }

  private boolean isPalindrome(String str) {
    for (int i = 0, j = str.length() - 1; i < j; i++, j--) {
      if (str.charAt(i) != str.charAt(j)) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/super-palindromes/submissions/937721694/){:target="_blank"}

# 설명
1. left와 right가 주어지면 그 사이의 숫자들 중 자기 자신과 제곱한 값이 앞 뒤가 같은 숫자(이하 회문)인 슈퍼 회문의 수를 계산하는 문제이다.

2. result에 left와 right가 9을 포함하는 경우이면 1을, 아니면 0을 넣어준다.

3. 1부터 최대 검증해야 하는 값인 $3^9 = 19684$까지 i를 증가시키며 아래를 수행한다.
- num에 i의 3진수 값을 넣어준다.
- num이 회문인 경우 아래를 수행한다.
  - square에 num의 제곱 값을 넣어준다.
  - square가 right를 초과하는 경우 범위를 벗어나 더 이상 검증할 필요가 없으므로, result를 주어진 문제의 결과로 반환한다.
  - square가 left 이상이고, 회문인 겨우 result를 증가시킨다.

4. 반복이 완료되면 [left, right] 범위 내 슈퍼 회문의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 해설
- left와 right는 최대 18 자리로, 회문의 구성의 절반은 9까지 존재한다.
- 자기 자신과 자기 자신의 제곱 수가 회문이 되기 위한 값들은 아래와 같다.
  - 1, 2, 3, 11, 22, 101, 111, 121, 202, 212, 1001, 1111, 2002, 10001, 10101, ...
- 위의 값들 중, 3을 제외하면 [0, 1, 2]로 구성이 되었으므로, 초기 result에 3의 제곱인 9가 존재하면 1로 아니면 0으로 초기화한다.
- 반복의 임계값이 19684인 이유는, 회문의 절반인 9자리까지 [0, 1, 2]의 세 값이 구성 가능하므로 $3^9$의 경우의 수를 사용하기 때문이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SuperPalindromes.java){:target="_blank"}에서 확인 가능합니다.