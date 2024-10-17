---
title: "Leetcode Java Least Operators to Express Number"
excerpt: "Leetcode Hard - 'Least Operators to Express Number' 문제 Java 풀이"
last_modified_at: 2023-08-01T19:40:00
header:
  image: /assets/images/leetcode/least-operators-to-express-number.png
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
[Link](https://leetcode.com/problems/least-operators-to-express-number){:target="_blank"}

# 코드
```java
class Solution {

  public int leastOpsExpressTarget(int x, int target) {
    int[] nums = new int[2];
    int i = 0;
    while (target > 0) {
      int curr = target % x;
      target /= x;
      if (i > 0) {
        nums = new int[] {
          Math.min((curr * i) + nums[0], ((curr + 1) * i) + nums[1]),
          Math.min(((x - curr) * i) + nums[0], ((x - curr - 1) * i) + nums[1])
        };
      } else {
        nums[0] = curr * 2;
        nums[1] = (x - curr) * 2;
      }
      i++;
    }
    return Math.min(nums[0], i + nums[1]) - 1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/least-operators-to-express-number/submissions/1009308375/){:target="_blank"}

# 설명
1. x로 target이 되기 위한 사칙 연산자의 최소 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- nums은 target이 되기 위한 사칙 연산자의 최소 갯수를 두 경우로 저장할 변수로, 크기가 2인 정수 배열로 초기화한다.
  - 처음 값은 target을 초과하지 않는 최대 횟수를, 마지막 값은 연산하는 총 횟수를 계산한다.
- i는 연산 횟수를 저장할 변수로, 0으로 초기화한다.

3. target이 0 초과일 때까지 아래를 반복한다.
- curr은 target을 x로 나눈 나머지를 저장하고, target에는 x를 나눈 몫을 저장한다.
- i가 0보다 큰 경우, nums에 아래를 순차적으로 계산하여 넣어준다.
  - nums의 첫 위치에 $(curr \times i) + nums[0]$와의 값과 $((curr + 1) \times i) + nums[1]$의 값 중 작은 값을 넣어준다.
  - nums의 다음 위치에 $((x - curr) \times i) + nums[0]$와의 값과 $((x - curr - 1) \times i) + nums[1]$의 값 중 작은 값을 넣어준다.
- 위의 경우가 아니라면 nums에 $curr \times 2$와 $(x - curr) \times 2$를 순차적으로 넣어준다.
- i를 증가시키고 다음 반복을 수행한다.

4. 반복이 완료되면 nums[0]과 $i + nums[1]$ 중 작은 값에 1을 뺀 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LeastOperatorsToExpressNumber.java){:target="_blank"}에서 확인 가능합니다.