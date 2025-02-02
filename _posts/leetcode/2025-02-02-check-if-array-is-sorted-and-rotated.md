---
title: "Leetcode Java Check if Array Is Sorted and Rotated"
excerpt: "Leetcode - 'Check if Array Is Sorted and Rotated' 문제 Java 풀이"
last_modified_at: 2025-02-02T14:30:00
header:
  image: /assets/images/leetcode/check-if-array-is-sorted-and-rotated.png
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
[Link](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean check(int[] nums) {
    int count = 0;
    int length = nums.length;
    for (int i = 0; i < length; i++) {
      if (nums[(i + 1) % length] < nums[i]) {
        count++;
      }
      if (count > 1) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/submissions/1528262502/){:target="_blank"}

# 설명
1. nums 배열을 회전하였을 때, 증가하는 숫자들로 이루어진 배열로 정렬이 가능한지 검증하는 문제이다.
- 배열 A를 x 위치로 회전시켜 만들어진 배열 B가 완성될 때, A[i] == B[($i + x$) % A.length]를 만족한다.
- % 연산 부호는 모듈러를 의미한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 주어진 조건인 A[i] == B[($i + x$) % A.length]를 만족하지 않고 더 작은 값이 되는 값의 갯수를 계산할 변수로, 0으로 초기화한다.
- length는 nums의 길이를 저장한 변수이다.

3. 0부터 length 미만까지 i를 증가시키면서 아래를 반복한다.
- nums[($i + x$) % A.length]의 값이 nums[i]보다 작은 오히려 값이 작아지는 경우, count를 증가시킨다.
- count가 둘 이상인 회전하더라도 조건을 만족하지 않는 경우, false를 주어진 문제의 결과로 반환한다.
  - count가 1인 경우, 그 지점을 기준으로 회전시키면 정렬이 가능하다.

4. 반복이 완료되면 회전을 통해 증가하는 배열로 변환 가능하므로 true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CheckIfArrayIsSortedAndRotated.java){:target="_blank"}에서 확인 가능합니다.