---
title: "Leetcode Java Maximal Score After Applying K Operations"
excerpt: "Leetcode Maximal Score After Applying K Operations Java"
last_modified_at: 2024-10-14T22:40:00
header:
  image: /assets/images/leetcode/maximal-score-after-applying-k-operations.png
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
[Link](https://leetcode.com/problems/maximal-score-after-applying-k-operations/){:target="_blank"}

# 코드
```java
class Solution {

  public long maxKelements(int[] nums, int k) {
    Queue<Integer> queue = new PriorityQueue<>(Collections.reverseOrder());
    for (int num : nums) {
      queue.add(num);
    }
    long result = 0;
    while (k-- > 0) {
      int num = queue.poll();
      result += num;
      queue.add((num + 2) / 3);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximal-score-after-applying-k-operations/submissions/1422047608/){:target="_blank"}

# 설명
1. nums 내 값들 중 k번 가장 큰 값을 3으로 나눈 값의 올림 값으로 치환할 때, 치환 대상 값들의 합을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- queue는 내림차순으로 값들을 저장할 변수로, PriorityQueue로 초기화하여 nums의 각 값들을 내림차순으로 넣어준다.
- result는 치환 대상 값들의 합을 저장할 변수로, long 형의 0으로 초기화한다.

3. k가 0 초과일 때 까지 아래를 반복하며 k를 감소시켜준다.
- num에 queue의 가장 앞의 큰 값을 꺼내 넣어준다.
- result에 num을 더하여 변환 대상의 값을 더해준다.
- queue에 올림을 위해서 $\frac{num + 2}{3}$의 값을 넣어준다.
  - ceil()은 올림 처리이므로, 3보다 1 작은 2를 더한 값에 3을 나눠 올림 처리와 같은 효과를 수행한다.

4. 반복이 완료되면 치환 대상 값들의 합이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximalScoreAfterApplyingKOperations.java){:target="_blank"}에서 확인 가능합니다.