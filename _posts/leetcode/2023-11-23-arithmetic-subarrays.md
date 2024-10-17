---
title: "Leetcode Java Arithmetic Subarrays"
excerpt: "Leetcode Medium - 'Arithmetic Subarrays II' 문제 Java 풀이"
last_modified_at: 2023-11-23T20:20:00
header:
  image: /assets/images/leetcode/arithmetic-subarrays.png
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
[Link](https://leetcode.com/problems/arithmetic-subarrays){:target="_blank"}

# 코드
```java
class Solution {

  public List<Boolean> checkArithmeticSubarrays(int[] nums, int[] l, int[] r) {
    List<Boolean> result = new ArrayList<>();
    for (int i = 0; i < l.length; i++) {
      result.add(this.checkArithmeticSubarrays(nums, l[i], r[i]));
    }
    return result;
  }

  private boolean checkArithmeticSubarrays(int[] nums, int left, int right) {
    if (right - left < 2) {
      return true;
    }
    int min = Integer.MAX_VALUE;
    int max = Integer.MIN_VALUE;
    for (int i = left; i <= right; i++) {
      min = Math.min(min, nums[i]);
      max = Math.max(max, nums[i]);
    }
    int diff = max - min;
    int length = right - left;
    if (diff % length != 0) {
      return false;
    }
    if (diff % length != 0) {
      return false;
    }
    diff /= length;
    if (diff == 0) {
      return true;
    }
    boolean[] visited = new boolean[length + 1];
    for (int i = left; i <= right; i++) {
      int value = nums[i] - min;
      if (value % diff != 0) {
        return false;
      } else {
        int index = value / diff;
        if (visited[index]) {
          return false;
        } else {
          visited[index] = true;
        }
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/arithmetic-subarrays/submissions/1104789697/){:target="_blank"}

# 설명
1. nums 내 [l[i], r[i]] 범위의 부분 배열로 [산술(등차) 수열](https://en.wikipedia.org/wiki/Arithmetic_progression){:target="_blank"}을 만들 수 있는지 검증하는 문제이다.

2. 결과를 넣을 result를 정의하고, l과 r의 처음부터 끝까지 값들을 이용하여 3번에서 정의한 checkArithmeticSubarrays(int[] nums, int left, int right)를 수행한 결과를 result에 넣어 주어진 문제의 결과로 반환한다.

3. [left, right] 범위 내 산술 수열을 검증하기 위한 checkArithmeticSubarrays(int[] nums, int left, int right) 메서드를 정의한다.
- $right - left$가 2 미만인 경우, 무조건 산술 수열이므로 true를 반환한다.
- min과 max에 위의 범위 내 최솟값과 최댓값을 넣어준다.
- diff는 $max - min$인 차잇값을, length는 $right - left$의 숫자 갯수를 넣어준다.
- diff에 length를 나눈 나머지 값이 0이 아닌 경우, 등차 수열을 이룰 수 없으므로 false를 반환한다.
- diff에 legnth를 나눈 값을 넣어주고 해당 값이 0인 경우, 등차 수열을 이룰 수 있으므로 true를 반환한다.
- visited는 동일한 값이 발생했는지 확인하기 위한 배열로, $length + 1$ 크기의 부울 배열로 초기화한다.
- left부터 right 이하까지 i를 증가시키며 아래를 반복한다.
  - value에 $nums[i] - min$인 등차 수열의 증가치를 넣어준다.
  - value를 diff로 나눈 나머지가 0이 아닌 경우 false를 반환한다.
  - 위의 경우가 아니라면 value를 diff로 나눈 값이 visited에 존재하면 false를 반환하고, 없으면 visited의 해당 위치 값을 true로 바꾸어준다.
- 반복이 완료되면 nums의 [left, right] 구간의 값들로 등차 수열을 이룰 수 있는지 검증이 완료되었으므로, true를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ArithmeticSubarrays.java){:target="_blank"}에서 확인 가능합니다.