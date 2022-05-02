---
title: "Leetcode Java Number Complement"
excerpt: "Leetcode Number Complement Java 풀이"
last_modified_at: 2022-05-02T13:00:00
header:
  image: /assets/images/leetcode/number-complement.png
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
[Link](https://leetcode.com/problems/number-complement/){:target="_blank"}

# 코드
```java
class Solution {

  public int findComplement(int num) {
    int sum = 1;
    while (sum < num) {
      sum = (sum << 1) | 1;
    }
    return sum - num;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/691349921/){:target="_blank"}

# 설명
1. num을 이진수로 변환하여 해당 보수로 변환된 정수를 반환하는 문제이다.
- 예를 들어, 5는 이진수로 101로 표현하며 해당 값의 보수는 010으로 2를 주어진 문제의 결과로 반환하면 된다.

2. num의 이진수를 모두 1로 변환한 값을 저장할 sum을 1로 저장한다.
- num의 최솟값은 1이므로, 해당 값부터 시작한다.

3. sum이 num보다 작을 때 까지 아래를 반복한다.
- sum에 sum의 비트를 좌측으로 1칸 이동시킨 값과 1의 OR(&#124;) 비트 연산의 결과를 넣어준다.

4. num의 이진수를 모두 1로 변환한 값에 num을 뺀 값이 보수가 되므로, 해당 값을 주어진 문제의 결과로 반환한다.
- 간단한 예로, $1010 = 1111 - 0101$ 이므로 1010(10)의 보수는 0101(5)이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberComplement.java){:target="_blank"}에서 확인 가능합니다.