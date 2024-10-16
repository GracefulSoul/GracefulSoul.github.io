---
title: "Leetcode Java Distribute Candies"
excerpt: "Leetcode Distribute Candies Java"
last_modified_at: 2022-07-16T09:00:00
header:
  image: /assets/images/leetcode/distribute-candies.png
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
[Link](https://leetcode.com/problems/distribute-candies/){:target="_blank"}

# 코드
```java
class Solution {

  public int distributeCandies(int[] candyType) {
    Set<Integer> types = new HashSet<>();
    for (int candy : candyType) {
      types.add(candy);
    }
    return Math.min(candyType.length / 2, types.size());
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/748137628/){:target="_blank"}

# 설명
1. candyType의 캔디를 절반을 먹을 때, 중복되지 않은 candy의 최대 유형 개수를 구하는 문제이다.

2. 중복을 배제한 캔디 유형의 개수를 저장하기 위한 types를 HashSet으로 초기화하고, candyType의 모든 값을 넣어준다.

3. candyType의 절반과 types의 크기 중 작은 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DistributeCandies.java){:target="_blank"}에서 확인 가능합니다.