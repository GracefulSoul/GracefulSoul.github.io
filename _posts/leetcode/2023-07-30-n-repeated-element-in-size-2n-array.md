---
title: "Leetcode Java N-Repeated Element in Size 2N Array"
excerpt: "Leetcode N-Repeated Element in Size 2N Array Java"
last_modified_at: 2023-07-30T13:00:00
header:
  image: /assets/images/leetcode/n-repeated-element-in-size-2n-array.png
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
[Link](https://leetcode.com/problems/n-repeated-element-in-size-2n-array){:target="_blank"}

# 코드
```java
class Solution {

  public int repeatedNTimes(int[] nums) {
    int length = nums.length;
    int n = length / 2;
    for (int i = 0; i < length; i++) {
      int count = 1;
      for (int j = i + 1; j < length; j++) {
        if (nums[i] == nums[j]) {
          count++;
        }
      }
      if (count == n) {
        return nums[i];
      }
    }
    return 0;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/n-repeated-element-in-size-2n-array/submissions/1007390058/){:target="_blank"}

# 설명
1. $2 \times n$ 크기로 구성된 정수 배열 nums 내 정확히 n번 반복되는 숫자를 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- n은 반복 횟수를 저장할 변수로, $\frac{length}{2}$로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- count는 반복 횟수를 저장할 변수로, 현재 위치까지 반복 횟수인 1로 초기화한다.
- $i + 1$부터 length 미만까지 아래를 수행한다.
  - nums의 i번째 숫자와 j번째 숫자가 같은 경우, count를 증가시킨다.
- 반복이 완료되고 count가 n인 경우는 해당 숫자를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 해당 조건을 만족하는 경우가 없으므로 0을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NRepeatedElementInSize2NArray.java){:target="_blank"}에서 확인 가능합니다.