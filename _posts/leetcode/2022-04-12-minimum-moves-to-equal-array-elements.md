---
title: "Leetcode Java Minimum Moves to Equal Array Elements"
excerpt: "Leetcode - 'Minimum Moves to Equal Array Elements' 문제 Java 풀이"
last_modified_at: 2022-04-12T12:00:00
header:
  image: /assets/images/leetcode/minimum-moves-to-equal-array-elements.png
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
[Link](https://leetcode.com/problems/minimum-moves-to-equal-array-elements/){:target="_blank"}

# 코드
```java
class Solution {

  public int minMoves(int[] nums) {
    int result = 0;
    int min = Integer.MAX_VALUE;
    for (int num : nums) {
      min = Math.min(min, num);
    }
    for (int num : nums) {
      result += num - min;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/678658646/){:target="_blank"}

# 설명
1. nums의 요소들을 동일한 값으로 만들기 위한 최소 횟수를 계산하는 문제이다.
- 한 번에 $n - 1$개의 요소의 값을 1씩 증가시킬 수 있다.

2. 주어진 문제 풀이에 필요한 변수를 정의한다.
- result는 최소 횟수를 저장하기 위한 변수로, 0으로 초기화한다.
- min은 nums 내 최솟값을 저장하기 위한 변수로, 정수의 가장 큰 값으로 초기화하고 nums를 반복하여 최솟값을 넣어준다.

3. nums를 반복하여 result에 $num - min$ 값을 더해준다.
- $n - 1$개의 요소를 1씩 증가시킬 수 있으므로, 현재 값에서 최솟값을 뺀 횟수만큼 증가하면 동일한 요소의 값으로 만들 수 있다.

4. 반복이 완료되면 최소 횟수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumMovesToEqualArrayElements.java){:target="_blank"}에서 확인 가능합니다.