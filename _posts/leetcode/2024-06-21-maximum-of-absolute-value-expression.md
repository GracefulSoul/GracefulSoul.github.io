---
title: "Leetcode Java Maximum of Absolute Value Expression"
excerpt: "Leetcode Medium - 'Maximum of Absolute Value Expression' 문제 Java 풀이"
last_modified_at: 2024-06-21T18:55:00
header:
  image: /assets/images/leetcode/maximum-of-absolute-value-expression.png
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
[Link](https://leetcode.com/problems/maximum-of-absolute-value-expression/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxAbsValExpr(int[] arr1, int[] arr2) {
    int result = Integer.MIN_VALUE;
    int i1 = -arr1[0] - arr2[0];
    int i2 = -arr1[0] + arr2[0];
    int i3 = arr1[0] - arr2[0];
    int i4 = arr1[0] + arr2[0];
    for (int i = 1; i < arr1.length; i++) {
      result = Math.max(result
          , Math.max(i1 + arr1[i] + arr2[i] + i
              , Math.max(i2 + arr1[i] - arr2[i] + i,
                  Math.max(i3 + -arr1[i] + arr2[i] + i
                      , i4 + -arr1[i] - arr2[i] + i))));
      i1 = Math.max(i1, -arr1[i] - arr2[i] - i);
      i2 = Math.max(i2, -arr1[i] + arr2[i] - i);
      i3 = Math.max(i3, arr1[i] - arr2[i] - i);
      i4 = Math.max(i4, arr1[i] + arr2[i] - i);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-of-absolute-value-expression/submissions/1295495354/){:target="_blank"}

# 설명
1. 정수 배열인 arr1과 arr2가 주어지면 아래 계산 공식을 만족하는 최대 값을 반환하는 문제이다.
- 계산 공식은 $|arr1[i] - arr1[j]| + |arr2[i] - arr2[j]| + |i - j|$이다.
- 0 <= i, j < arr1.legnth를 만족한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과를 저장할 변수로, 0으로 초기화한다.
- i1은 $arr1[i] <= arr1[j] && arr2[i] <= arr2[j]$를 만족하는 경우로, 아래의 공식을 활용하여 계산된다.
  - $arr1[j] - arr1[i] + arr2[j] - arr2[i] + j - i = (arr1[j] + arr2[j] + j) + (-arr1[i] - arr2[i] - i)$
  - 현재 위치의 값은 $-arr1[i] - arr2[i] - i$로 계산하여 첫 값인 $-arr1[0] - arr2[0]$을 넣어준다.
- i2는 $arr1[i] <= arr1[j] && arr2[i] >= arr2[j]$를 만족하는 경우로, 아래의 공식을 활용하여 계산된다.
  - $arr1[j] - arr1[i] + arr2[i] - arr2[j] + j - i = (arr1[j] - arr2[j] + j) + (-arr1[i] + arr2[i] - i)$
  - 현재 위치의 값은 $-arr1[i] + arr2[i] - i$로 계산하여 첫 값인 $-arr1[0] + arr2[0]$을 넣어준다.
- i3는 $arr1[i] >= arr1[j] && arr2[i] <= arr2[j]$를 만족하는 경우로, 아래의 공식을 활용하여 계산된다.
  - $arr1[i] - arr1[j] + arr2[j] - arr2[i] + j - i = (-arr1[j] + arr2[j] + j) + (arr1[i] - arr2[i] - i)$
  - 현재 위치의 값은 $arr1[i] - arr2[i] - i$로 계산하여 첫 값인 $arr1[0] - arr2[0]$을 넣어준다.
- i4는 $arr1[i] >= arr1[j] && arr2[i] >= arr2[j]$를 만족하는 경우로, 아래의 공식을 활용하여 계산된다.
  - $arr1[i] - arr1[j] + arr2[i] - arr2[j] + j - i = (-arr1[j] - arr2[j] + j) + (arr1[i] + arr2[i] - i)$
  - 현재 위치의 값은 $arr1[i] - arr2[i] - i$로 계산하여 첫 값인 $arr1[0] + arr2[0]$을 넣어준다.

3. 1부터 arr1의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- result에 result와 아래의 각 경우 중 큰 값을 넣어준다.
  - i1의 계산 공식인 이전 위치의 값과 현재 위치의 값의 합인 $i1 + arr1[i] + arr2[i] + i$의 값.
  - i2의 계산 공식인 이전 위치의 값과 현재 위치의 값의 합인 $i2 + arr1[i] - arr2[i] + i$의 값.
  - i3의 계산 공식인 이전 위치의 값과 현재 위치의 값의 합인 $i3 + -arr1[i] + arr2[i] + i$의 값.
  - i4의 계산 공식인 이전 위치의 값과 현재 위치의 값의 합인 $i4 + -arr1[i] - arr2[i] + i$의 값.
- i1부터 i4에 이전 위치에서 계산한 값과 현재 위치에서 계산한 값 중 큰 값을 각각 넣어준다.

4. 반복이 완료되면 결과가 계산된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumOfAbsoluteValueExpression.java){:target="_blank"}에서 확인 가능합니다.