---
title: "Leetcode Java Number of Segments in a String"
excerpt: "Leetcode Number of Segments in a String Java 풀이"
last_modified_at: 2022-03-26T20:00:00
header:
  image: /assets/images/leetcode/number-of-segments-in-a-string.png
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
[Link](https://leetcode.com/problems/number-of-segments-in-a-string/){:target="_blank"}

# 코드
```java
class Solution {

  public int countSegments(String s) {
    s = s.trim();
    int length = s.length();
    char[] charArray = s.toCharArray();
    int count = 0;
    if (length == 0) {
      return count;
    } else {
      for (int idx = 0; idx < length; idx++) {
        if (charArray[idx] == ' ' && charArray[idx + 1] != ' ') {
          count++;
        }
      }
      return count + 1;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/667549397/){:target="_blank"}

# 설명
1. 문자열 s가 주어지면 해당 문자열의 세그먼트의 수를 반환하는 문제이다.
- 단, 세그먼트는 공백이 아닌 문자로 이루어진 문자열이다.

2. 우선 문자열 s의 불필요한 좌우 공백을 제거해준다.

3. 문제 풀이에 필요한 변수를 정의한다.
- length는 좌우 공백을 제거한 s의 길이를 저장할 변수로, s의 길이로 초기화한다.
- charArray는 자우 공백을 제거한 s를 문자 배열로 변환하여 사용할 변수로, s를 문자 배열로 변환하여 넣어준다.
- count는 세그먼트 수를 계산할 변수로, 0으로 초기화한다.

4. length가 0인 경우 세그먼트 또한 없으므로, 0을 주어진 문제의 결과로 반환한다.

5. length가 0이 아닌 경우, 아래를 수행하여 세그먼트 수를 계산하여 $count + 1$을 주어진 문제의 결과로 반환한다.
- 0부터 length 미만까지 idx를 증가시키며 idx번째 문자가 공백이고, $idx + 1$ 번쨰 문자가 공백이 아닌 세그먼트 시작 부분을 확인하면 count를 증가시킨다.
- count가 아니라 $count + 1$을 반환하는 이유는, 처음 세그먼트를 count에 반영하지 않았기 때문이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfSegmentsInAString.java){:target="_blank"}에서 확인 가능합니다.