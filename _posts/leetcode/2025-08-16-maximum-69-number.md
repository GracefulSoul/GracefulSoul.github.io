---
title: "Leetcode Java Maximum 69 Number"
excerpt: "Leetcode - 'Maximum 69 Number' 문제 Java 풀이"
last_modified_at: 2025-08-16T10:20:00
header:
  image: /assets/images/leetcode/maximum-69-number.png
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
[Link](https://leetcode.com/problems/maximum-69-number/){:target="_blank"}

# 코드
```java
class Solution {

  public int maximum69Number(int num) {
    int position = -1;
    for (int i = 0, temp = num, remainder = temp % 10; temp > 1; i++, temp /= 10, remainder = temp % 10) {
      if (remainder == 6) {
        position = i;
      }
    }
    if (-1 < position) {
      num += (int) (3 * Math.pow(10, position));
    }
    return num;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-69-number/submissions/1736770689/){:target="_blank"}

# 설명
1. 6과 9로 이루어진 num을 최대 한 자리만 바꿔서 최대가 되는 값으로 변경하는 문제이다.

2. position은 위치를 바꿀 자릿수를 저장할 변수로, -1로 초기화한다.

3. i에 0, temp에 num, remainder에 temp의 1의 자릿수를 넣고 temp가 1보다 클 때까지 i를 증가시키고, remainder에 temp의 1의 자릿수를 넣어주며 아래를 반복한다.
- remainder가 6인 경우, position에 현재 자릿수인 i를 넣어준다.

4. position이 -1보다 큰 변경 가능한 위치가 존재하는 경우, num에 $10^position$ 값을 더해준다.

5. 수행이 완료되어 최대 한 자리만 바꾸어 가능한 최대 값으로 변환된 num을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/Maximum69Number.java){:target="_blank"}에서 확인 가능합니다.