---
title: "Leetcode Java Minimum Number of Days to Make m Bouquets"
excerpt: "Leetcode Minimum Number of Days to Make m Bouquets Java"
last_modified_at: 2024-06-19T21:50:00
header:
  image: /assets/images/leetcode/minimum-number-of-days-to-make-m-bouquets.png
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
[Link](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/){:target="_blank"}

# 코드
```java
class Solution {

  public int minDays(int[] bloomDay, int m, int k) {
    if ((long) m * k > bloomDay.length) {
      return -1;
    }
    int left = 1;
    int right = (int) 1e9;
    while (left < right) {
      int mid = left + (right - left) / 2;
      if (this.isPossibleMakeBouquets(bloomDay, m, k, mid)) {
        right = mid;
      } else {
        left = mid + 1;
      }
    }
    return left;
  }

  private boolean isPossibleMakeBouquets(int[] bloomDay, int m, int k, int day) {
    int total = 0;
    int length = bloomDay.length;
    for (int i = 0; i < length; i++) {
      int count = 0;
      while (i < length && count < k && bloomDay[i] <= day) {
        count++;
        i++;
      }
      if (count == k) {
        total++;
        i--;
      }
      if (total >= m) {
        return true;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/submissions/1293321614/){:target="_blank"}

# 설명
1. 각 꽃의 개화일이 담긴 bloomDay를 이용하여 한 번씩만 사용하여 k개의 인접한 꽃을 이용하여 m개의 꽃다발을 만들 때, 만들 수 있는 최소 일수를 구하는 문제이다.
- 단, 만들 수 없는 경우 -1을 주어진 문제의 결과로 반환한다.

2. $m \times k$가 bloomDay의 길이보다 커서 인접한 꽃을 한 번씩만 사용하여 꽃다발을 만들 수 없는 경우, -1을 주어진 문제의 결과로 반환한다.

3. 일자 탐색에 필요한 변수인 left와 right에 left는 최소 개화일인 1, right는 최대 개화일인 $10^9$로 초기화한다.

4. left가 right 미만일 때 까지 아래를 반복한다.
- mid에 $left + \frac{right - left} / 2$인 중앙값을 넣어준다.
- 5번에서 정의한 isPossibleMakeBouquets(int[] bloomDay, int m, int k, int day)인 꽃다발을 만들 수 있는 경우, right에 mid를 아니면 left에 $mid + 1$을 넣어 개화일 탐색 범위을 좁혀준다.

5. bloomDay 내 k개의 인접한 꽃을 이용하여 m개의 꽃다발을 만들 수 있는지 검증하기 위한 isPossibleMakeBouquets(int[] bloomDay, int m, int k, int day) 메서드를 정의한다.
- 문제 풀이에 필요한 변수를 정의한다.
  - total은 총 꽃다발의 갯수를 계산할 변수로, 0으로 초기화한다.
  - length는 bloomDay의 길이를 저장한 변수이다.
- 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
  - count는 꽃의 갯수를 계산할 변수로, 0으로 초기화한다.
  - i가 length 미만이면서 count가 k개 미만이고, bloomDay[i] 값이 day 이하인 꽃다발에 꽃을 넣을 수 있을 때 까지 count와 i를 증가시킨다.
  - count가 k인 꽃다발이 완성된 경우, total인 꽃다발의 갯수를 증가시키고 i를 감소시킨다.
  - total이 m 이상이면 m개의 꽃다발이 완성되었으므로, true를 반환한다.
- 반복이 완료되면 꽃다발을 완성할 수 없으므로, false를 반환한다.

6. 반복이 완료되면 최소 일수가 저장된 left를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumNumberOfDaysToMakeMBouquets.java){:target="_blank"}에서 확인 가능합니다.