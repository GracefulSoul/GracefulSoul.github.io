---
title: "Leetcode Java Find Score of an Array After Marking All Elements"
excerpt: "Leetcode - 'Find Score of an Array After Marking All Elements' 문제 Java 풀이"
last_modified_at: 2024-12-13T19:50:00
header:
  image: /assets/images/leetcode/find-score-of-an-array-after-marking-all-elements.png
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
[Link](https://leetcode.com/problems/find-score-of-an-array-after-marking-all-elements/){:target="_blank"}

# 코드
```java
class Solution {

  public long findScore(int[] nums) {
    int length = nums.length;
    Integer[] dp = new Integer[length];
    for (int i = 0; i < length; i++) {
      dp[i] = i;
    }
    Arrays.sort(dp, (a, b) -> nums[a] - nums[b]);
    long result = 0;
    boolean[] marked = new boolean[length + 2];
    for (int i : dp) {
      if (!marked[i + 1]) {
        marked[i] = marked[i + 2] = true;
        result += nums[i];
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-score-of-an-array-after-marking-all-elements/submissions/1477724240/){:target="_blank"}

# 설명
1. nums에서 아래 순서대로 반복할 때 선택된 값들의 합을 구하는 문제이다.
- 가장 작은 값 하나를 선택하고 마크한다.
- 해당 값 좌우 값 중 존재하는 값들을 마크한다.
- 마크되지 않은 값들 중 가장 작은 값을 선택하여 마크하고 바로 위 순서를 모든 값들이 마크될 때 까지 반복한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- dp는 각 순서에 대한 값을 저장할 배열로, 정수 배열로 초기화하여 각 위치별 0-index 값을 넣은 후 nums의 크기 순 오름차순으로 정렬해준다.
- result는 합계를 저장할 변수로, 0으로 초기화한다.
- marked는 마크된 값을 저장할 변수로, $length + 2$ 크기로 초기화한다.

3. dp의 값들을 순차적으로 i에 넣어 아래를 수행한다.
- marked[i + 1]의 값이 false인 마크되지 않은 값인 경우, 아래를 수행한다.
  - marked의 i번째 값과 $i + 2$번째 값인 좌우 값을 true를 넣어 마크한다.
  - result에 nums[i]인 선택된 값을 더해준다.

4. 반복이 완료되면 합계가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindScoreOfAnArrayAfterMarkingAllElements.java){:target="_blank"}에서 확인 가능합니다.