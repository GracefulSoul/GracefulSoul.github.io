---
title: "Leetcode Java Best Sightseeing Pair"
excerpt: "Leetcode Best Sightseeing Pair Java"
last_modified_at: 2023-12-19T21:30:00
header:
  image: /assets/images/leetcode/best-sightseeing-pair.png
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
[Link](https://leetcode.com/problems/best-sightseeing-pair){:target="_blank"}

# 코드
```java
class Solution {

  public int maxScoreSightseeingPair(int[] values) {
    int result = 0;
    int max = 0;
    for (int i = 0; i < values.length; i++) {
      result = Math.max(result, max + values[i] - i);
      max = Math.max(max, values[i] + i);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/best-sightseeing-pair/submissions/1123366305/){:target="_blank"}

# 설명
1. values의 i < j를 만족하는 두 위치의 값을 이용하여 $values[i] + values[j] + i - j$가 최대가 되는 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 최대가 되는 값을 저장할 변수로, 0으로 초기화한다.
- max는 위치 값과 해당 값의 합이 최대인 값을 저장하기 위한 변수로, 0으로 초기화한다.

3. 0부터 values의 길이 미만까지 i를 증가시키며 아래를 수행한다.
- result에 result와 이전까지 가장 큰 값과 위치 값을 가진 max에 $values[i] - i$의 값 중 큰 값을 넣어준다.
- max에 max와 $values[i] + i$ 중 큰 값을 다시 넣어준다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BestSightseeingPair.java){:target="_blank"}에서 확인 가능합니다.