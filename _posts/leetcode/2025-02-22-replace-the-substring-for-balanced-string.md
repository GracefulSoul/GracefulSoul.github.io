---
title: "Leetcode Java Replace the Substring for Balanced String"
excerpt: "Leetcode - 'Replace the Substring for Balanced String' 문제 Java 풀이"
last_modified_at: 2025-02-22T15:50:00
header:
  image: /assets/images/leetcode/replace-the-substring-for-balanced-string.png
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
[Link](https://leetcode.com/problems/replace-the-substring-for-balanced-string/){:target="_blank"}

# 코드
```java
class Solution {

  public int balancedString(String s) {
    int[] counts = new int[128];
    for (char c : s.toCharArray()) {
      counts[c]++;
    }
    int length = s.length();
    int max = length / 4;
    int result = length;
    int i = 0;
    for (int j = 0; j < length; j++) {
      counts[s.charAt(j)]--;
      while (i < length && counts['Q'] <= max && counts['W'] <= max && counts['E'] <= max && counts['R'] <= max) {
        result = Math.min(result, j - i + 1);
        counts[s.charAt(i++)]++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/replace-the-substring-for-balanced-string/submissions/1551435925/){:target="_blank"}

# 설명
1. 'Q', 'W', 'E', 'R' 문자로 구성된 문자열 s가 균등한 문자의 배분이 되도록 하기 위한 최소 부분 문자열의 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- counts는 각 문자의 갯수를 계산하기 위한 변수로, 128 크기의 정수 배열로 초기화하고 s의 각 문자 갯수를 넣어준다.
- length는 s의 길이를 저장한 변수이다.
- max는 각 문자의 상한 갯수를 저장할 변수로, $\frac{length}{4}$로 초기화한다.
- result는 결과를 저장할 변수로, 최대 부분 문자열의 길이인 length로 초기화한다.
- i는 변환 문자의 시작 부분을 저장할 변수로, 0으로 초기화한다.

3. 0부터 length 미만까지 j를 증가시키며 아래를 반복한다.
- counts 내 s의 j번째 문자에 해당하는 갯수를 감소시킨다.
- i가 length 미만이면서, counts 내 'Q', 'W', 'E', 'R'의 해당하는 갯수가 max 이하일 때 까지 아래를 반복한다.
  - result에 result와 $j - i + 1$ 중 변환 갯수 중 작은 값을 저장한다.
  - counts의 s내 i번째 문자에 해당하는 값을 증가시켜 변환 갯수를 복구시켜주고, i도 증가시켜 다음 문자열로 이동시켜준다.

4. 반복이 완료되면 최소 부분 문자열의 길이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReplaceTheSubstringForBalancedString.java){:target="_blank"}에서 확인 가능합니다.