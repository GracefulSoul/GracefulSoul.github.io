---
title: "Leetcode Java Maximize Happiness of Selected Children"
excerpt: "Leetcode Maximize Happiness of Selected Children Java"
last_modified_at: 2024-05-09T19:50:00
header:
  image: /assets/images/leetcode/maximize-happiness-of-selected-children.png
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
[Link](https://leetcode.com/problems/maximize-happiness-of-selected-children/){:target="_blank"}

# 코드
```java
class Solution {

  public long maximumHappinessSum(int[] happiness, int k) {
    Arrays.sort(happiness);
    long result = 0;
    int length = happiness.length;
    for (int i = length - 1, j = 0; i >= length - k; i--) {
      result += Math.max(0, happiness[i] - j++);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximize-happiness-of-selected-children/submissions/1253461931/){:target="_blank"}

# 설명
1. 각 아이들의 행복 값이 저장된 happiness에서 k개의 아이를 선택하여 발생할 수 있는 최대의 행복 값을 구하는 문제이다.
- 행복의 정도는 음수가 될 수 없으며, 한 아이를 고를 경우 다른 아이들의 행복 값이 1 감소한다.

2. happiness를 오름차순 정렬해준다.

3. 문제풀이에 필요한 변수를 정의한다.
- result는 결과 값인 행복 값의 합을 저장할 변수로, 0으로 초기화한다.
- length는 happiness의 길이를 저장한 변수이다.

4. $length - 1$부터 i가 $length - k$보다 클 때 까지 i를 감소시키고 j는 0으로 초기화시켜 아래를 반복한다.
- result에 0과 $happiness[i] - j$의 값 중 큰 값을 넣고 j를 증가시켜준다.

5. 반복이 완료되면 k명의 행복의 값이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximizeHappinessOfSelectedChildren.java){:target="_blank"}에서 확인 가능합니다.