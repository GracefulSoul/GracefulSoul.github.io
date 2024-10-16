---
title: "Leetcode Java Partition Array Into Three Parts With Equal Sum"
excerpt: "Leetcode Partition Array Into Three Parts With Equal Sum Java"
last_modified_at: 2023-12-16T10:00:00
header:
  image: /assets/images/leetcode/partition-array-into-three-parts-with-equal-sum.png
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
[Link](https://leetcode.com/problems/partition-array-into-three-parts-with-equal-sum){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canThreePartsEqualSum(int[] arr) {
    int sum = 0;
    for (int num : arr) {
      sum += num;
    }
    if (sum % 3 != 0) {
      return false;
    }
    int average = sum / 3;
    sum = 0;
    int count = 0;
    for (int num : arr) {
      sum += num;
      if (sum == average) {
        sum = 0;
        count++;
        if (count == 3) {
          return true;
        }
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/partition-array-into-three-parts-with-equal-sum/submissions/1120680803/){:target="_blank"}

# 설명
1. arr의 연속된 값들을 3등분하여 각 부분 배열의 합이 동일한 값으로 나눌 수 있는지 검증하는 문제이다.

2. sum에 arr의 모든 값을 더해서 넣어준 후 해당 값을 3으로 정확히 나눌 수 있는지 검증하여 불가능한 경우, false를 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- average는 3등분 기준 값을 넣을 변수로, sum을 3으로 나눈 값을 넣어준다.
- sum을 부분 합을 저장하기 위해서 0으로 초기화한다.
- count는 부분 배열의 수를 저장할 변수로, 0으로 초기화한다.

4. arr의 모든 값을 차례대로 num에 넣어 아래를 반복한다.
- sum에 num을 더해준다.
- sum이 average와 동일한 경우, 아래를 수행한다.
  - 다음 부분 합을 계산하기 위해서 sum을 0으로 초기화 후, count를 증가시킨다.
  - count가 3이면 arr의 값들을 동일한 값으로 3등분 가능하므로, true를 주어진 문제의 결과로 반환한다.

5. 반복이 완료되면 arr의 값들을 동일한 값으로 3등분할 수 없으므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PartitionArrayIntoThreePartsWithEqualSum.java){:target="_blank"}에서 확인 가능합니다.