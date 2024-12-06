---
title: "Leetcode Java Maximum Number of Integers to Choose From a Range I"
excerpt: "Leetcode - 'Maximum Number of Integers to Choose From a Range I' 문제 Java 풀이"
last_modified_at: 2024-12-06T17:40:00
header:
  image: /assets/images/leetcode/maximum-number-of-integers-to-choose-from-a-range-i.png
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
[Link](https://leetcode.com/problems/maximum-number-of-integers-to-choose-from-a-range-i/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxCount(int[] banned, int n, int maxSum) {
    boolean[] ban = new boolean[10001];
    for (int num : banned) {
      ban[num] = true;
    }
    long sum = 0;
    int count = 0;
    for (int i = 1; i <= n; i++) {
      if (!ban[i]) {
        sum += i;
        if (sum > maxSum) {
          break;
        }
        count++;
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/move-pieces-to-obtain-a-string/submissions/1471697531/){:target="_blank"}

# 설명
1. [1, n] 범위의 숫자들 중 banned 내 숫자들을 제외하고 maxSum 이하의 합계를 구하기 위한 숫자들의 최대 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- ban은 banned의 값 유무를 저장하기 위한 변수로, 상한값인 $10^4$보다 1 큰 크기의 부울 배열로 초기화하여 존재하는 값의 위치를 true로 변경한다.
- sum은 합계를 저장할 변수로, 0으로 초기화한다.
- count는 합계를 수행한 숫자 갯수를 저장할 변수로, 0으로 초기화한다.

3. 1부터 n 이하까지 i를 증가시키면서 아래를 반복한다.
- ban[i]가 false인 금지된 숫자가 아닌 경우, 아래를 수행한다.
  - sum에 i를 더한 후 sum이 maxSum보다 큰 경우, 반복을 중지한다.
  - count를 증가시켜 더한 값의 갯수를 증가시켜준다.

4. 반복이 완료되면 계산된 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumNumberOfIntegersToChooseFromARangeI.java){:target="_blank"}에서 확인 가능합니다.