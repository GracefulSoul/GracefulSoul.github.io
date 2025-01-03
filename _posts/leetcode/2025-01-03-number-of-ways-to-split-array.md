---
title: "Leetcode Java Number of Ways to Split Array"
excerpt: "Leetcode - 'Number of Ways to Split Array' 문제 Java 풀이"
last_modified_at: 2025-01-03T12:20:00
header:
  image: /assets/images/leetcode/number-of-ways-to-split-array.png
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
[Link](https://leetcode.com/problems/number-of-ways-to-split-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int waysToSplitArray(int[] nums) {
    int length = nums.length;
    long left = 0;
    long right = 0;
    for (int num : nums) {
      right += num;
    }
    int result = 0;
    for (int i = 0; i < length - 1; i++) {
      left += nums[i];
      right -= nums[i];
      if (left >= right) {
        result++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-ways-to-split-array/submissions/1495755516/){:target="_blank"}

# 설명
1. nums 내 값들을 특정 위치를 기준으로 두 부분 집합으로 분리할 때, 좌측 부분 집합의 합이 우측 부분 집합의 합보다 크거나 같게 분리할 수 있는 방법의 갯수를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- left와 right는 좌측과 우측 부분 집합의 합을 저장할 변수로, 0과 num의 합계를 순차적으로 넣어준다.
- result는 분리할 수 있는 방법의 갯수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 $length - 1$ 미만까지 i를 증가시키며 아래를 반복한다.
- left에 nums[i] 값을 더해주고, right에 nums[i] 값을 빼준다.
- left가 right 이상인 분리 가능한 경우, result를 증가시켜준다.

4. 반복이 완료되어 계산된 방법의 갯수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfWaysToSplitArray.java){:target="_blank"}에서 확인 가능합니다.