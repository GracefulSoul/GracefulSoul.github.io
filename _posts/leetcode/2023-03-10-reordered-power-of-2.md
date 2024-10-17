---
title: "Leetcode Java Reordered Power of 2"
excerpt: "Leetcode - 'Reordered Power of 2' 문제 Java 풀이"
last_modified_at: 2023-03-10T19:45:00
header:
  image: /assets/images/leetcode/reordered-power-of-2.png
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
[Link](https://leetcode.com/problems/reordered-power-of-2){:target="_blank"}

# 코드
```java
class Solution {

  public boolean reorderedPowerOf2(int n) {
    long count = this.getCount(n);
    for (int i = 0; i < 32; i++) {
      if (this.getCount(1 << i) == count) {
        return true;
      }
    }
    return false;
  }

  private long getCount(int n) {
    long count = 0;
    while (n > 0) {
      count += (int) Math.pow(10, n % 10);
      n /= 10;
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/reordered-power-of-2/submissions/912626766/){:target="_blank"}

# 설명
1. 앞의 자리가 0이 되지 않도록 순서를 변경하여 2의 거듭 제곱이 될 수 있도록 할 수 있는지 검증하는 문제이다.

2. count에 3번에서 정의한 getCount(int n) 메서드에 n을 넣어 수행한 결과를 넣어준다.

3. 주어진 숫자의 0 ~ 9 까지 숫자의 개수를 계산할 getCount(int n) 메서드를 정의한다.
- count는 숫자의 개수를 계산할 변수로, overflow를 방지하기 위해서 long 타입의 0으로 초기화한다.
- n이 0 초과일 때 까지 아래를 수행한다.
  - count에 n을 10으로 나눈 값의 나머지를 이용하여 10의 제곱수를 더해준다.
  - n에 n을 10으로 나눈 몫을 넣어준다.
- 반복이 완료되면 계산된 count를 반환한다.

4. 0부터 32 미만까지 i를 증가시키며 아래를 반복한다.
- 1의 비트를 좌측으로 i만큼 이동한 값을 이용하여 3번에서 정의한 getCount(int n) 메서드를 수행한 결과가 count와 동일하면 거듭 제곱이 가능하므로, true를 주어진 문제의 결과로 반환한다.

5. 반복이 완료되면 거듭 제곱을 만들 수 없으므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReorderedPowerOf2.java){:target="_blank"}에서 확인 가능합니다.