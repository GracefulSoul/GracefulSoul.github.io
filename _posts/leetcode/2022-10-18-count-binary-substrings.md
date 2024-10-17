---
title: "Leetcode Java Count Binary Substrings"
excerpt: "Leetcode - 'Count Binary Substrings' 문제 Java 풀이"
last_modified_at: 2022-10-18T19:00:00
header:
  image: /assets/images/leetcode/count-binary-substrings.png
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
[Link](https://leetcode.com/problems/count-binary-substrings){:target="_blank"}

# 코드
```java
class Solution {

  public int countBinarySubstrings(String s) {
    int prev = 0;
    int curr = 1;
    int result = 0;
    char[] charArray = s.toCharArray();
    for (int idx = 1; idx < s.length(); idx++) {
      if (charArray[idx - 1] == charArray[idx]) {
        curr++;
      } else {
        result += Math.min(curr, prev);
        prev = curr;
        curr = 1;
      }
    }
    return result + Math.min(curr, prev);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/825101498/){:target="_blank"}

# 설명
1. 0과 1인 이진 값으로 구성된 s를 이용하여 0과 1의 수가 동일한 부분 문자열의 수를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- prev는 이전 이진 값의 반복 횟수를 저장하기 위한 변수로, 0으로 초기화한다.
- curr은 현재 이진 값의 반복 횟수를 저장하기 위한 변수로, 첫 값을 포함하여 1로 초기화한다.
- result는 0과 1의 수가 동일한 부분 문자열의 수를 계산하기 위한 변수로, 0으로 초기화한다.
- charArray는 s를 문자 배열로 저장한 변수이다.

3. 1부터 s의 길이 미만까지 idx를 증가시키며 아래를 반복한다.
- charArray의 $idx - 1$번째 문자와 idx번째 문자가 동일한 경우, curr을 증가시킨다.
- 위의 경우가 아니라면 이진 값이 변경된 위치이므로 아래를 수행한다.
  - result에 curr과 prev 중 작은 값인 0과 1이 동일하게 반복된 횟수를 넣어준다.
  - prev에 현재 값의 반복 횟수인 curr을 넣은 후 다음 이진 값의 반복 횟수인 curr을 1로 초기화한다.

4. 3번에서 계산된 result와 마지막으로 반복 횟수인 curr와 prev 중 작은 값을 더해서 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountBinarySubstrings.java){:target="_blank"}에서 확인 가능합니다.