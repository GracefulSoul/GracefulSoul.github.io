---
title: "Leetcode Java Sequential Digits"
excerpt: "Leetcode Medium - 'Sequential Digits' 문제 Java 풀이"
last_modified_at: 2024-02-02T19:00:00
header:
  image: /assets/images/leetcode/sequential-digits.png
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
[Link](https://leetcode.com/problems/sequential-digits){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> sequentialDigits(int low, int high) {
    int[] nums = {
      12, 23, 34, 45, 56, 67, 78, 89,
      123, 234, 345, 456, 567, 678, 789,
      1234, 2345, 3456, 4567, 5678, 6789,
      12345, 23456, 34567, 45678, 56789,
      123456, 234567, 345678, 456789,
      1234567, 2345678, 3456789,
      12345678, 23456789,
      123456789
    };
    List<Integer> result = new ArrayList<>();
    int length = nums.length;
    for (int i = 0; i < length; i++) {
      if (nums[i] < low) {
        continue;
      } else if (nums[i] > high) {
        break;
      } else {
        result.add(nums[i]);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sequential-digits/submissions/1163787210/){:target="_blank"}

# 설명
1. [low, high] 범위 내 0을 제외한 이전 자리의 값보다 다음 자리의 값이 큰 순차적인 정수들을 오름차순으로 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- nums는 모든 가능한 숫자의 범위를 저장한 변수로, 최소 가능한 12부터 최대 가능한 123456789까지 경우의 수를 모두 넣어준다.
- result는 결과를 저장할 변수로, ArrayList로 초기화한다.
- length는 nums의 길이를 저장한 변수이다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- nums[i] 값이 low보다 작은 경우 대상에서 제외되므로, 다음 반복을 수행한다.
- nums[i] 값이 high보다 큰 경우 범위를 초과하였으므로, 반복을 중단한다.
- 위의 경우들이 모두 아닌 범위 내 값이면, result에 nums[i] 값을 넣어준다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SequentialDigits.java){:target="_blank"}에서 확인 가능합니다.