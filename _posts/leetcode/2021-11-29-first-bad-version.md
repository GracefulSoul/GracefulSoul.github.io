---
title: "Leetcode Java First Bad Version"
excerpt: "Leetcode - 'First Bad Version' 문제 Java 풀이"
last_modified_at: 2021-11-29T20:00:00
header:
  image: /assets/images/leetcode/first-bad-version.png
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
[Link](https://leetcode.com/problems/first-bad-version/){:target="_blank"}

# 코드
```java
public class Solution extends VersionControl {

  public int firstBadVersion(int n) {
    int low = 1;
    int high = n;
    while (low < high) {
      int mid = low + ((high - low) / 2);
      if (isBadVersion(mid)) {
        high = mid;
      } else {
        low = mid + 1;
      }
    }
    return low;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/594394246/){:target="_blank"}

# 설명
1. 주어진 정수인 n은 제품의 버전으로, VersionControl 클래스에서 제공되는 isBadVersion 메서드를 활용하여 최소의 검사를 통해 첫 번째로 잘못된 버전을 찾는 문제이다.

2. 문제의 풀이에 필요한 변수를 정의한다.
- low는 binary search를 활용하여 최소 버전부터 탐색하기 위한 변수로, 1로 초기화한다.
- high는 binary search를 활용하여 최대 버전부터 탐색하기 위한 변수로, n으로 초기화한다.

3. low가 high보다 클 때 까지 반복하여 검증을 수행한다.
- mid에 low를 보정치로 사용한 $low + \frac{high - low}{2}$의 결과를 넣어준다.
- mid를 이용하여 isBadVersion 메서드를 호출한 결과가 true인 경우, high에 mid를 넣어 최대 버전의 범위를 축소한다.
- mid를 이용하여 isBadVersion 메서드를 호출한 결과가 false인 경우, low에 $mid + 1$을 넣어 최소 버전의 범위를 축소한다.

4. 반복이 완료되면 최소 버전인 low를 첫 번째로 잘못된 버전으로 인지하고, 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FirstBadVersion.java){:target="_blank"}에서 확인 가능합니다.