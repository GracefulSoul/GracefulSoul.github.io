---
title: "Leetcode Java Summary Ranges"
excerpt: "Leetcode Summary Ranges Java 풀이"
last_modified_at: 2021-11-03T12:00:00
header:
  image: /assets/images/leetcode/summary-ranges.png
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
[Link](https://leetcode.com/problems/summary-ranges/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> summaryRanges(int[] nums) {
    List<String> result = new ArrayList<>();
    for (int idx = 0; idx < nums.length; idx++) {
      int num = nums[idx];
      while (idx < nums.length - 1 && nums[idx] == nums[idx + 1] - 1) {
        idx++;
      }
      if (num == nums[idx]) {
        result.add(String.valueOf(num));
      } else {
        result.add(String.join("->", String.valueOf(num), String.valueOf(nums[idx])));
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/581248420/){:target="_blank"}

# 설명
1. 주어진 중복된 정수가 없는 오르참순으로 정렬된 배열인 nums를 이용하여 숫자들의 요약된 범위를 만드는 문제이다.
- [a, b]에서 a와 b가 같지 않을 경우, "a->b"로 표현한다.
- [a, b]에서 a와 b가 같은 경우, "a"로 표현한다.
- 예를 들어 [0, 1, 2, 4, 6, 7]의 경우, ["0->2", "4", "6->7"]로 표현이 된다.

2. 주어진 문제의 결과를 담기 위해 result를 List로 정의한다.

3. nums를 반복하여 숫자들의 요약된 범위를 result에 넣어준다.
- num에 nums[idx]값을 임시 저장시킨다.
- idx가 $nums.length - 1$이하이고, nums[idx]의 값과 $nums[idx + 1] - 1$의 값이 같을 때 까지 idx를 증가시켜 연속된 숫자들을 축약한다.
- 임시 저장한 num의 값과 nums[idx] 값이 같을 경우, result에 num의 값을 String으로 변환하여 넣어준다.
- 임시 저장한 num의 값과 nums[idx] 값이 다를 경우, result에 num과 nums[idx]의 값을 이용하여 "num->nums[idx]"형태로 넣어준다.

4. 반복이 종료되면 숫자들의 요약된 범위를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SummaryRanges.java){:target="_blank"}에서 확인 가능합니다.