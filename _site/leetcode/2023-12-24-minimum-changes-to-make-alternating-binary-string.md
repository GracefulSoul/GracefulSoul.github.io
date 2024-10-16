---
title: "Leetcode Java Minimum Changes To Make Alternating Binary String"
excerpt: "Leetcode Minimum Changes To Make Alternating Binary String Java"
last_modified_at: 2023-12-24T09:10:00
header:
  image: /assets/images/leetcode/minimum-changes-to-make-alternating-binary-string.png
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
[Link](https://leetcode.com/problems/minimum-changes-to-make-alternating-binary-string){:target="_blank"}

# 코드
```java
class Solution {

  public int minOperations(String s) {
    int result = 0;
    int length = s.length();
    for (int i = 0; i < length; i++) {
      if ((i % 2) != s.charAt(i) - '0') {
        result++;
      }
    }
    return Math.min(result, length - result);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-changes-to-make-alternating-binary-string/submissions/1126979044/){:target="_blank"}

# 설명
1. 0과 1로만 이루어진 s를 동일한 숫자가 연속되어 나타나지 않도록 재배열할 때, 바꿔야하는 최소한의 문자 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 바꿀 문자의 갯수를 저장할 변수로, 0으로 초기화하한ㄷ.
- length는 s의 길이를 지정한 변수이다.

3. 0부터 length까지 홀수 위치에 '1'이, 짝수 위치에 '0'이 존재하는지 검증하여 해당 갯수를 result에 넣어준다.

4. 반복이 완료되면 result의 반대 경우인 홀수 위치에 '0'이, 짝수 위치에 '1'이 존재하는 경우에 대한 갯수인 $length - result$와 result 중 작은 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumChangesToMakeAlternatingBinaryString.java){:target="_blank"}에서 확인 가능합니다.