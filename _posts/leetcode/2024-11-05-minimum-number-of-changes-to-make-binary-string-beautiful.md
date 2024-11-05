---
title: "Leetcode Java Minimum Number of Changes to Make Binary String Beautiful"
excerpt: "Leetcode - 'Minimum Number of Changes to Make Binary String Beautiful' 문제 Java 풀이"
last_modified_at: 2024-11-05T21:50:00
header:
  image: /assets/images/leetcode/minimum-number-of-changes-to-make-binary-string-beautiful.png
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
[Link](https://leetcode.com/problems/minimum-number-of-changes-to-make-binary-string-beautiful/){:target="_blank"}

# 코드
```java
class Solution {

  public int minChanges(String s) {
    char[] charArray = s.toCharArray();
    int result = 0;
    for (int i = 0; i < charArray.length - 1; i += 2) {
      if (charArray[i] != charArray[i + 1]) {
        result++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-number-of-changes-to-make-binary-string-beautiful/submissions/1443795208/){:target="_blank"}

# 설명
1. s의 각 문자열을 두 문자씩 잘라서 둘 다 1 혹은 0으로 만들기 위한 최소 횟수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s를 문자 배열로 변환한 변수이다.
- result는 최소 횟수를 계산할 변수로, 0으로 초기화한다.

3. 0부터 charAaray의 길이보다 1 작은 값 미만까지 2씩 증가시키며 아래를 수행한다.
- charArray[i]와 charArray[$i + 1$]이 다르면 둘 중 하나의 값을 바꿔야 하므로, result를 증가시킨다.

4. 반복이 완료되면 최소 횟수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumNumberOfChangesToMakeBinaryStringBeautiful.java){:target="_blank"}에서 확인 가능합니다.