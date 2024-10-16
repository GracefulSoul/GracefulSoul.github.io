---
title: "Leetcode Java Distribute Candies to People"
excerpt: "Leetcode Distribute Candies to People Java"
last_modified_at: 2024-05-04T20:40:00
header:
  image: /assets/images/leetcode/distribute-candies-to-people.png
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
[Link](https://leetcode.com/problems/distribute-candies-to-people/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] distributeCandies(int candies, int num_people) {
    int[] result = new int[num_people];
    for (int i = 0; candies > 0; i++) {
      result[i % num_people] += Math.min(candies, i + 1);
      candies -= i + 1;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/distribute-candies-to-people/submissions/1248870486/){:target="_blank"}

# 설명
1. num_people의 사람들에게 순차적으로 1개부터 1개씩 증가시키며 candies의 사탕을 줄 때, 사람들 별 받은 사탕의 갯수를 반환하는 문제이다.
- 마지막 사람까지 사탕을 받으면 다시 첫 사람부터 사탕의 갯수를 계속 증가시키며 제공한다.

2. result는 결과를 저장할 배열로, num_people 크기의 정수 배열로 초기화한다.

3. 0부터 candies의 갯수가 0 초과일 때 까지 i를 증가시키며 아래를 반복한다.
- result의 $\frac{i}{num_people}$의 나머지 값에 해당하는 위치에 candies와 $i + 1$ 중 작은 값을 넣어준다.
- candies에 제공된 $i + 1$개를 차감해준다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DistributeCandiesToPeople.java){:target="_blank"}에서 확인 가능합니다.