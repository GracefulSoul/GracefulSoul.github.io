---
title: "Leetcode Java Maximum Value of an Ordered Triplet II"
excerpt: "Leetcode - 'Maximum Value of an Ordered Triplet II' 문제 Java 풀이"
last_modified_at: 2025-04-03T18:00:00
header:
  image: /assets/images/leetcode/maximum-value-of-an-ordered-triplet-ii.png
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
[Link](https://leetcode.com/problems/maximum-value-of-an-ordered-triplet-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public long maximumTripletValue(int[] nums) {
    long result = 0;
    long diff = 0;
    long max = 0;
    for (int num : nums) {
      result = Math.max(result, diff * num);
      diff = Math.max(diff, max - num);
      max = Math.max(max, num);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-value-of-an-ordered-triplet-ii/submissions/1595383632/){:target="_blank"}

# 설명
1. 양의 정수로 구성된 nums의 임의 i < j < k 를 만족하는 세 위치 i, j, k를 이용하여 $(nums[i] - nums[j]) \times nums[k]$의 값이 최대인 값을 구하는 문제이다.
- 이전 문제 [Maximum Value of an Ordered Triplet I](../maximum-value-of-an-ordered-triplet-i){:target="_blank"}와 유사한 문제로, 배열의 길이가 더 늘어난 문제이다.
- 단, 결과가 음의 정수이면 0을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 최댓값을 저장하기 위한 변수로, long 타입의 0으로 초기화한다.
- diff는 $nums[i] - nums[j]$의 값이 최대인 값을 구하기 위한 변수로, num과 곱한 값이 매우 클 수 있으므로 long 타입의 0으로 초기화한다.
- max는 마지막 곱하기 위한 nums[k]의 값을 구하기 위한 변수로, diff를 저장 할 수 있는 long 타입의 0으로 초기화한다.

3. nums의 값들을 순차적으로 num에 넣고 아래를 수행한다.
- result에 result와 $diff \times num$을 long 타입으로 변환한 값 중 큰 값을 넣어준다.
- diff에 diff와 $max - num$ 중 차잇값이 큰 값을 넣어준다.
- max에는 max와 num 중 큰 값을 넣어 곱할 값을 넣어준다.

4. 반복이 완료되어 조건을 만족하는 최댓값이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumValueOfAnOrderedTripletII.java){:target="_blank"}에서 확인 가능합니다.