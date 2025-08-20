---
title: "Leetcode Java Element Appearing More Than 25% In Sorted Array"
excerpt: "Leetcode - 'Element Appearing More Than 25% In Sorted Array' 문제 Java 풀이"
last_modified_at: 2025-08-20T18:30:00
header:
  image: /assets/images/leetcode/element-appearing-more-than-25-in-sorted-array.png
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
[Link](https://leetcode.com/problems/element-appearing-more-than-25-in-sorted-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int findSpecialInteger(int[] arr) {
    int length = arr.length;
    int quarter = length / 4;
    for (int i = 0; i < length - quarter; i++) {
      if (arr[i] == arr[i + quarter]) {
        return arr[i];
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/element-appearing-more-than-25-in-sorted-array/submissions/1741844368/){:target="_blank"}

# 설명
1. 오름차순으로 정렬된 arr 내 숫자들 중 $\frac{1}{4}$ 이상 존재하는 숫자를 찾아 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 arr 길이를 저장한 변수이다.
- quarter는 arr 길이의 $\frac{1}{4}$ 값을 저장한 변수이다.

3. 0부터 $length - quarter$ 미만까지 i를 증가시키며 아래를 반복한다.
- arr[i] 값과 arr[$i + quarter$] 값이 동일한 arr 길이의 $\frac{1}{4}$ 구간 이상의 값이 동일한 경우, arr[i] 값을 주어진 문제의 결과로 반환한다.

4. arr 길이의 $\frac{1}{4}$ 이상 존재하는 값이 없는 경우, -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ElementAppearingMoreThan25PercentInSortedArray.java){:target="_blank"}에서 확인 가능합니다.