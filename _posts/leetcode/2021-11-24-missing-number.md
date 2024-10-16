---
title: "Leetcode Java Missing Number"
excerpt: "Leetcode Missing Number Java 풀이"
last_modified_at: 2021-11-24T09:00:00
header:
  image: /assets/images/leetcode/missing-number.png
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
[Link](https://leetcode.com/problems/missing-number/){:target="_blank"}

# 코드
```java
class Solution {

  public int missingNumber(int[] nums) {
    int total = 0;
    int length = nums.length;
    for (int num : nums) {
      total += num;
    }
    return ((length * (length + 1)) / 2) - total;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/591720832/){:target="_blank"}

# 설명
1. 주어진 배열 nums에 누락된 숫자를 찾는 문제이다.
- 단, nums에 누락된 숫자가 없을 경우 다음 이어지는 숫자를 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- total은 주어진 배열 nums의 숫자를 더하기 위한 변수로, 0으로 초기화한다.
- length는 주어진 배열 nums의 길이를 저장하기 위한 변수이다.

3. nums 배열 내 모든 값을 total에 저장한다.

4. length를 이용하여 0부터 $length + 1$까지 숫자들의 합한 값에 total의 값을 뺀 숫자를 주어진 문제의 결과로 반환한다.
- 0부터 $n + 1$까지 합한 값은 $\frac{(n \times (n + 1))}{2}$의 공식의 결과로 확인 할 수 있다.
- 아래에 발생 가능한 두 가지 경우를 예를 든다.
  - nums = [0, 1, 3, 4]인 경우, $\frac{(4 \times (4 + 1))}{2} - (0 + 1 + 3 + 4) = 10 - 8 = 2$로 누락된 값인 <b>2</b>이 주어진 문제의 결과가 된다.
  - nums = [0, 1, 2, 3]인 경우, $\frac{(4 \times (4 + 1))}{2} - (0 + 1 + 2 + 3) = 10 - 6 = 4$로 다음 이어지는 숫자인 <b>4</b>가 주어진 문제의 결과가 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MissingNumber.java){:target="_blank"}에서 확인 가능합니다.