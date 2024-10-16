---
title: "Leetcode Java Minimum Index Sum of Two Lists"
excerpt: "Leetcode Minimum Index Sum of Two Lists Java"
last_modified_at: 2022-07-28T19:20:00
header:
  image: /assets/images/leetcode/minimum-index-sum-of-two-lists.png
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
[Link](https://leetcode.com/problems/minimum-index-sum-of-two-lists/){:target="_blank"}

# 코드
```java
class Solution {

  public String[] findRestaurant(String[] list1, String[] list2) {
    Map<String, Integer> map = new HashMap<>();
    List<String> result = new ArrayList<>();
    int min = Integer.MAX_VALUE;
    for (int idx = 0; idx < list1.length; idx++) {
      map.put(list1[idx], idx);
    }
    for (int idx = 0; idx < list2.length && idx <= min; idx++) {
      if (map.containsKey(list2[idx])) {
        int sum = idx + map.get(list2[idx]);
        if (sum < min) {
          result.clear();
          result.add(list2[idx]);
          min = sum;
        } else if (sum == min) {
          result.add(list2[idx]);
        }
      }
    }
    return result.toArray(new String[result.size()]);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/758905194/){:target="_blank"}

# 설명
1. 좋아하는 음식점 순위가 담긴 list1과 list2 중 가장 우선 순위가 높은 음식점을 찾는 문제이다.
- 단, 동일한 순위의 음식점이 존재하면 해당 음식점들을 모두 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 list1의 음식점의 순위를 담을 변수로, HashMap으로 초기화한다.
- result는 동일한 우선 순위의 음식점들을 담을 변수로, ARrayList로 초기화한다.
- min은 최소 순위를 저장할 변수로, 정수의 최댓값으로 초기화한다.

3. list1을 반복하여 map에 음식점 별 순위를 0부터 차례대로 넣어준다.

4. 0부터 lst2의 길이 미만이며 idx가 min이하일 때 까지 idx를 증가시키며 아래를 반복한다.
- map에 list2의 idx번째 음식점이 존재하지 않으면 다음 반복을 수행한다.
- sum에 idx와 map에서 list2의 idx번째 음식점의 순위 합산을 넣어준다.
- sum이 min 미만인 경우, result를 초기화하고 위의 음식점을 넣어준다.
- sum이 min과 동일한 경우, result에 위의 음식점을 넣어준다.

5. 반복이 완료되면 우선 순위가 높은 음식점들을 저장한 result를 배열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumIndexSumOfTwoLists.java){:target="_blank"}에서 확인 가능합니다.