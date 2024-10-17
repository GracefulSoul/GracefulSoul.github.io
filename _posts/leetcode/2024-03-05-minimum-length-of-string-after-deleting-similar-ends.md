---
title: "Leetcode Java Minimum Length of String After Deleting Similar Ends"
excerpt: "Leetcode Medium - 'Minimum Length of String After Deleting Similar Ends' 문제 Java 풀이"
last_modified_at: 2024-03-05T20:10:00
header:
  image: /assets/images/leetcode/minimum-length-of-string-after-deleting-similar-ends.png
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
[Link](https://leetcode.com/problems/minimum-length-of-string-after-deleting-similar-ends){:target="_blank"}

# 코드
```java
class Solution {

  public int minimumLength(String s) {
    char[] charArray = s.toCharArray();
    int left = 0;
    int right = s.length() - 1;
    while (left < right && charArray[left] == charArray[right]) {
      char c = s.charAt(left);
      while (left <= right && charArray[left] == c) {
        left++;
      }
      while (left <= right && charArray[right] == c) {
        right--;
      }
    }
    return right - left + 1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-length-of-string-after-deleting-similar-ends/submissions/1194642090/){:target="_blank"}

# 설명
1. 'a', 'b', 'c'로 이루어진 문자열 s를 이용하여 아래의 규칙을 만족하는 최소 문자열의 길이을 구하는 문제이다.
- 문자열 s의 앞과 뒤에 동일한 문자가 존재하면, 앞과 뒤에 연속된 동일 문자들을 모두 제거해준다.
- 문자열 s의 앞과 뒤에 동일한 문자가 존재하지 않으면 반복을 그만한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s를 문자 배열로 변환한 변수이다.
- left와 right는 charArray 내 좌측과 우측의 위치 변수로, 시작 위치인 0과 종료 위치인 $s.length - 1$로 초기화한다.

4. left가 right보다 작으면서 charArray의 left번째 문자와 right번째 문자가 동일할 때까지 아래를 반복한다.
- c에 charArray의 left번째 문자를 넣어준다.
- left가 right보다 작거나 같으면서 charArray의 left번째 문자가 c와 동일할 때까지 left를 증가시켜 동일한 문자를 제거한다.
- left가 right보다 작거나 같으면서 위와 반대로 charArray의 right번째 문자가 c와 동일할 때까지 right를 감소시켜 동일한 문자를 제거한다.

5. 반복이 완료되면 남은 문자열의 길이인 $right - left + 1$를 주어진 문제의 길이로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumLengthOfStringAfterDeletingSimilarEnds.java){:target="_blank"}에서 확인 가능합니다.