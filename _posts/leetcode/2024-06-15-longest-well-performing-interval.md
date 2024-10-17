---
title: "Leetcode Java Longest Well-Performing Interval"
excerpt: "Leetcode Medium - 'Longest Well-Performing Interval' 문제 Java 풀이"
last_modified_at: 2024-06-15T09:50:00
header:
  image: /assets/images/leetcode/longest-well-performing-interval.png
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
[Link](https://leetcode.com/problems/longest-well-performing-interval/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestWPI(int[] hours) {
    int result = 0;
    int sum = 0;
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < hours.length; i++) {
      sum += hours[i] > 8 ? 1 : -1;
      if (sum > 0) {
        result = i + 1;
      } else {
        map.putIfAbsent(sum, i);
        if (map.containsKey(sum - 1)) {
          result = Math.max(result, i - map.get(sum - 1));
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/longest-well-performing-interval/submissions/1288586813/){:target="_blank"}

# 설명
1. 업무 시간이 저장된 hours를 이용하여 양호한 수행 구간의 길이를 반환하는 문제이다.
- 양호한 수행 기간은 업무 시간이 8시간 초과인 일자가 더 많은 구간이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 양호한 수행 구간의 길이를 저장할 변수로, 0으로 초기화한다.
- sum은 양호한 수행 기간 중 8시간 초과인 일자의 수를 계산할 변수로, 0으로 초기화한다.
- map은 양호한 수행 기간을 계산하기 위한 변수로, HashMap으로 초기화한다.

3. 0부터 hours의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- sum을 hors[i]의 값이 8시간 초과이면 증가, 이하이면 감소시켜준다.
- sum이 0보다 크면 양호한 수행 구간이므로, result에 $i + 1$을 넣어준다.
- sum이 0과 같거나 작으면 양호한 수행 구간이 아니므로, 아래를 수행한다.
  - map에 sum의 위치에 i를 넣어 저장해준다.
  - map에 $sum - 1$의 값이 존재하면 해당 위치부터 현재까지 값이 양호한 수행 구간을 만족하므로, result에 result와 $i - map.get(sum - 1)$에 대한 값을 뺀 차잇값 중 큰 값을 넣어준다.

4. 반복이 완료되면 양호한 수행 구간의 길이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestWellPerformingInterval.java){:target="_blank"}에서 확인 가능합니다.