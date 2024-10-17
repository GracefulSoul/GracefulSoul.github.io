---
title: "Leetcode Java Maximum Width Ramp"
excerpt: "Leetcode Medium - 'Maximum Width Ramp' 문제 Java 풀이"
last_modified_at: 2023-07-31T19:20:00
header:
  image: /assets/images/leetcode/maximum-width-ramp.png
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
[Link](https://leetcode.com/problems/maximum-width-ramp){:target="_blank"}

# 코드
```java
class Solution {

  public int maxWidthRamp(int[] nums) {
    int length = nums.length;
    Stack<Integer> stack = new Stack<>();
    for (int i = 0; i < length; i++) {
      if (stack.empty() || nums[i] < nums[stack.peek()]) {
        stack.push(i);
      }
    }
    int result = 0;
    for (int i = length - 1; i >= 0; i--) {
      while (!stack.empty() && nums[stack.peek()] <= nums[i]) {
        result = Math.max(i - stack.pop(), result);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-width-ramp/submissions/1008386806/){:target="_blank"}

# 설명
1. 아래의 조건을 만족하는 최대 길이를 구하는 문제이다.
- 두 위치 i < j에서 nums[i] <= nums[j]의 최대 길이는 $j - 1$이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- stack은 최대 길이를 계산하기 위한 변수로, stack으로 초기화하고 아래를 이용하여 값을 넣어준다.
  - 0부터 length 미만까지 i를 증가시키며, stack이 비어있거나 nums의 i번째 값이 nums에서 stack의 첫 값보다 작을 경우 stack에 i를 넣어준다.
- result는 최대 길이를 저장할 변수로, 0으로 초기화한다.

3. $length - 1$부터 0 이상까지 i를 증가시키며 아래를 수행한다.
- stack이 비어있지 않고 nums의 stack의 첫 값이 nums의 i번째 값보다 작거나 같은 경우, result에 i에서 stack의 값을 뺀 값과 result 중 큰 값인 최대 길이를 넣어준다.

4. 반복이 완료되면 최대 길이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumWidthRamp.java){:target="_blank"}에서 확인 가능합니다.