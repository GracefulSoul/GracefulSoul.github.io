---
title: "Leetcode Java Flip String to Monotone Increasing"
excerpt: "Leetcode Flip String to Monotone Increasing Java"
last_modified_at: 2023-05-22T18:45:00
header:
  image: /assets/images/leetcode/flip-string-to-monotone-increasing.png
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
[Link](https://leetcode.com/problems/flip-string-to-monotone-increasing){:target="_blank"}

# 코드
```java
class Solution {

  public int minFlipsMonoIncr(String s) {
    int flip0 = 0;
    int flip1 = 0;
    for (char c : s.toCharArray()) {
      int num = c - '0';
      flip0 += num;
      flip1 = Math.min(flip0, flip1 + 1 - num);
    }
    return flip1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/flip-string-to-monotone-increasing/submissions/955015620/){:target="_blank"}

# 설명
1. 0과 1로 구성된 s를 이용하여 점층적으로 증가하는 문자열로 변환하는데 필요한 최소 변환 횟수를 구하는 문제이다.

2. flip0과 flip1는 값을 변환한 횟수를 저장할 변수로, 둘 다 0으로 초기화한다.

3. s의 처음부터 끝까지 각 문자를 c에 넣어 아래를 반복한다.
- num에 c를 숫자로 변환하여 넣어준다.
- flip0에 1 -> 0으로 변환한 횟수인 num을 더해준다.
- flip1에는 0 -> 1로 변환한 횟수인 $flip1 + 1 - num$의 값과 flip0 중 작은 값을 넣어준다.

4. 반복이 완료되면 최소 변환 횟수가 저장된 flip1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FlipStringToMonotoneIncreasing.java){:target="_blank"}에서 확인 가능합니다.