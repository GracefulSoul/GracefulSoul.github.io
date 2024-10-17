---
title: "Leetcode Java Separate Black and White Balls"
excerpt: "Leetcode Medium - 'Separate Black and White Balls' 문제 Java 풀이"
last_modified_at: 2024-10-15T19:10:00
header:
  image: /assets/images/leetcode/separate-black-and-white-balls.png
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
[Link](https://leetcode.com/problems/separate-black-and-white-balls/){:target="_blank"}

# 코드
```java
class Solution {

  public long minimumSteps(String s) {
    char[] charArray = s.toCharArray();
    long result = 0;
    for (int i = 0, j = 0; i < charArray.length; i++) {
      if (charArray[i] == '0') {
        result += i - (j++);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/separate-black-and-white-balls/submissions/1423036470/){:target="_blank"}

# 설명
1. 문자열 s 내 검정색 공은 '1', 흰 공은 '0'을 뜻하며 인접한 공을 선택하여 교체할 때 검정색 공을 오른쪽으로, 흰 공은 왼쪽으로 모으기 위한 최소 횟수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s를 문자 배열로 변환한 변수이다.
- result는 최소 교체 횟수를 계산할 변수로, 0으로 초기화한다.

3. 0부터 charArray의 길이 미만까지 i를 증가시키며, 흰 공의 갯수은 j는 0으로 초기화하여 아래를 반복한다.
- charArray[i]가 '0'인 흰 공인 경우, result에 $i - j$인 현재 위치에서 흰 공을 좌측으로 이동하기 위한 변환 횟수를 더해준 후 흰 공의 갯수인 j를 증가시켜준다.

4. 반복이 완료되면 최소 교체 횟수가 계산된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximalScoreAfterApplyingKOperations.java){:target="_blank"}에서 확인 가능합니다.