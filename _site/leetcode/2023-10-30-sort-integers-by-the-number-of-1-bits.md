---
title: "Leetcode Java Sort Integers by The Number of 1 Bits"
excerpt: "Leetcode Sort Integers by The Number of 1 Bits Java"
last_modified_at: 2023-10-30T12:20:00
header:
  image: /assets/images/leetcode/sort-integers-by-the-number-of-1-bits.png
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
[Link](https://leetcode.com/problems/sort-integers-by-the-number-of-1-bits){:target="_blank"}

# 코드
```java
class Solution {

  public int[] sortByBits(int[] arr) {
    int length = arr.length;
    for (int i = 0; i < length; i++) {
      arr[i] += Integer.bitCount(arr[i]) * 10001;
    }
    Arrays.sort(arr);
    for (int i = 0; i < length; i++) {
      arr[i] %= 10001;
    }
    return arr;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sort-integers-by-the-number-of-1-bits/submissions/1087247278/){:target="_blank"}

# 설명
1. arr의 값들을 bit로 변환한 값의 1의 갯수가 작은 값순서로 값들을 오름차순 정렬하는 문제이다.
- [0, 1, 2, 3, 4, 5, 6, 7, 8]의 값을 예를 들어보자.
  - 1의 갯수가 1개인 [1, 2, 4, 8]
  - 1의 갯수가 2개인 [3, 5, 6]
  - 1의 갯수가 3개인 [7]
  - 위를 이어주면 [1, 2, 4, 8, 3, 5, 6, 7]이 된다.

2. length는 arr의 길이를 저장한 값이다.

3. 0부터 length 미만까지 i를 증가시키며 arr[i]의 값에 arr[i]의 비트 수를 10001로 곱한 값을 더해준다.
- 값의 범위는 [0, $10^4$]이므로, 범위의 상한을 넘는 모듈러 형식으로 사용하기 위한 값으로 $10^4 + 1$을 사용한다.

4. arr의 값을 오름차순으로 정렬한 후, 0부터 length 미만까지 i를 증가시키며 arr[i]의 값을 10001로 나눈 나머지를 넣어 원래 값으로 복원한 후 arr을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SortIntegersByTheNumberOf1Bits.java){:target="_blank"}에서 확인 가능합니다.