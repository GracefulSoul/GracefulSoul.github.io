---
title: "Leetcode Java Find Lucky Integer in an Array"
excerpt: "Leetcode - 'Find Lucky Integer in an Array' 문제 Java 풀이"
last_modified_at: 2025-07-05T20:00:00
header:
  image: /assets/images/leetcode/find-lucky-integer-in-an-array.png
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
[Link](https://leetcode.com/problems/find-lucky-integer-in-an-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int findLucky(int[] arr) {
    int[] counts = new int[501];
    for (int num : arr) {
      counts[num]++;
    }
    for (int i = arr.length; i > 0; i--) {
      if (i == counts[i]) {
        return i;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-lucky-integer-in-an-array/submissions/1687734521/){:target="_blank"}

# 설명
1. arr 내 숫자와 갯수가 일치하는 값 중 가장 큰 값을 반환하는 문제이다.
- 단, 조건에 해당하는 숫자가 없으면 -1을 주어진 문제의 결과로 반환한다.

2. counts는 arr 내 값의 갯수를 계산하기 위한 변수로, 값의 상한인 500보다 1 큰 정수 배열로 초기화 후 arr 내 숫자에 해당하는 위치에 갯수를 넣어준다.

3. arr의 길이부터 0 초과일 때 까지 i를 감소시키며, i 와 counts[i]의 값이 동일한 경우 해당 값을 반환한다.

4. 반복이 완료되면 조건에 해당하는 숫자가 없으므로, -1을 주어진 문제의 결과로 반환한다.

# 해설
- arr 내 값의 상한과 arr의 길이 제한이 500 이하이므로, arr 길이를 초과하는 숫자에 해당하는 갯수는 존재할 수 없다.
- 발생 가능한 arr의 길이부터 내림차순으로 조건을 확인하여, 먼저 조건을 만족하는 숫자가 가장 큰 값이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindLuckyIntegerInAnArray.java){:target="_blank"}에서 확인 가능합니다.