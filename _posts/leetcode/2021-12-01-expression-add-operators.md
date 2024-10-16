---
title: "Leetcode Java Expression Add Operators"
excerpt: "Leetcode Expression Add Operators Java 풀이"
last_modified_at: 2021-12-01T22:00:00
header:
  image: /assets/images/leetcode/expression-add-operators.png
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
[Link](https://leetcode.com/problems/expression-add-operators/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> addOperators(String num, int target) {
    List<String> result = new ArrayList<>();
    if (Long.valueOf(num) > Integer.MAX_VALUE) {
      return result;
    }
    char[] nums = num.toCharArray();
    char[] path = new char[nums.length * 2 - 1];
    long val = 0;
    for (int idx = 0; idx < nums.length; idx++) {
      val = val * 10 + nums[idx] - '0';
      path[idx] = nums[idx];
      this.recursive(result, target, nums, path, 0, val, idx + 1, idx + 1);
      if (val == 0) {
        break;
      }
    }
    return result;
  }

  private void recursive(List<String> result, int target, char[] nums, char[] path, long left, long right, int numsIdx, int pathIdx) {
    if (numsIdx == nums.length) {
      if (left + right == target) {
        result.add(new String(path, 0, pathIdx));
      }
      return;
    }
    long val = 0;
    int j = pathIdx + 1;
    for (int i = numsIdx; i < nums.length; i++) {
      val = val * 10 + nums[i] - '0';
      path[j++] = nums[i];
      path[pathIdx] = '+';
      this.recursive(result, target, nums, path, left + right, val, i + 1, j);
      path[pathIdx] = '-';
      this.recursive(result, target, nums, path, left + right, -val, i + 1, j);
      path[pathIdx] = '*';
      this.recursive(result, target, nums, path, left, right * val, i + 1, j);
      if (nums[numsIdx] == '0') {
        return;
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/595409731/){:target="_blank"}

# 설명
1. 숫자로 구성된 주어진 문자열 num을 이용하여 각 숫자 간 연산을 이용하여 target을 만들기 위한 모든 연산식을 찾는 문제이다.

2. 주어진 연산식을 넣을 컬렉션인 result를 정의하고, 만일 num을 Long으로 변환한 값이 Integer를 초과하는 경우 result를 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- nums는 num을 문자의 배열로 변환하여 저장하기 위한 변수이다.
- path는 nums의 길이의 2배보다 1 작은 크기로 문자 배열을 정의한다.
- val은 문자열 num을 숫자로 변환하여 저장하기 위한 변수이다.

4. nums 배열을 처음부터 끝까지 반복하여 result에 연산식을 넣어준다.
- val에 $val \times 10$의 값과 nums[idx]에 '0'을 빼서 숫자로 전환한 값을 합쳐서 넣어준다.
- path[idx]에 nums[idx] 값을 넣어준다.
- 아래의 재귀 호출을 활용하여 result를 완성한다.

5. nums의 index를 나타내는 numsIdx가 nums의 길이와 동일한 경우 아래를 수행한다.
- $left + right$ 값이 target이 되는지 확인하여, path를 이용하여 path에 저장된 index인 pathIdx 위치 값까지 문자열로 전환하여 result에 넣어준다.
- return을 통해 재귀 호출을 끝내준다.

6. val에 0을, j에 $pathIdx + 1$ 값을 넣어 numsIdx부터 nums까지 아래를 반복한다.
- val에 $val \times 10$의 값과 nums[idx]에 '0'을 빼서 숫자로 전환한 값을 합쳐서 넣어준다.
- path[j]에 nums[i] 값을 넣어주고, j를 증가시킨다.
- path[pathIdx]에 '+'를, left에 $left + right$의 값을, right에 val을, numsIdx를 증가시켜 재귀 호출을 수행한다.
- path[pathIdx]에 '-'를, left에 $left + right$의 값을, right에 -val을, numsIdx를 증가시켜 재귀 호출을 수행한다.
- path[pathIdx]에 '*'를, right에 $right \times val$의 값을, numsIdx를 증가시켜 재귀 호출을 수행한다.
- nums[numsIdx]의 값이 '0'인 경우, 재귀 호출을 종료한다.

7. val 값이 0인지 확인하여 반복문을 종료시킨다.

8. 반복문이 종료되면 연산식이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ExpressionAddOperators.java){:target="_blank"}에서 확인 가능합니다.