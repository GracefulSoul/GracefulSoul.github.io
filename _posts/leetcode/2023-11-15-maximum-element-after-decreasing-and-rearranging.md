---
title: "Leetcode Java Maximum Element After Decreasing and Rearranging"
excerpt: "Leetcode Maximum Element After Decreasing and Rearranging Java"
last_modified_at: 2023-11-15T19:20:00
header:
  image: /assets/images/leetcode/maximum-element-after-decreasing-and-rearranging.png
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
[Link](https://leetcode.com/problems/maximum-element-after-decreasing-and-rearranging){:target="_blank"}

# 코드
```java
class Solution {

  public int maximumElementAfterDecrementingAndRearranging(int[] arr) {
    int length = arr.length;
    int[] count = new int[length];
    for (int i = 0; i < length; i++) {
      count[Math.min(arr[i] - 1, length - 1)]++;
    }
    int result = 1;
    for (int i = 1; i < length; i++) {
      result = Math.min(i + 1, result + count[i]);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-element-after-decreasing-and-rearranging/submissions/1099324660/){:target="_blank"}

# 설명
1. 양의 정수 배열 arr을 이용하여 아래의 조건과 연산을 수행하여 최댓값을 반환하는 문제이다.
- arr의 첫 값은 1로 시작해야한다.
- 인접한 값들의 차이는 1 이하여야 한다.
- 위의 조건에 맞도록 여러 번 연산할 수 있는 작업은 아래와 같다.
  - arr의 값이라도 최대한 작은 정수로 만든다.
  - arr의 값들을 임의 순서로 재배치한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 arr의 길이를 저장한 변수이다.
- count는 숫자 계산에 필요한 배열로, 1부터 시작하므로 가장 큰 값인 length 크기의 정수 배열로 초기화하고 0부터 legnth까지 i를 증가시키며 count의 $arr[i] - 1$과 $length - 1$ 중 작은 위치의 값을 증가시킨다.
- result는 최댓값을 저장할 변수로, 시작 값인 1로 초기화한다.

3. 1부터 length 미만까지 i를 증가시키며 result에 $i + 1$과 $result + count[i]$ 중 작은 값을 넣어준다.

4. 반복이 완료되면 최댓값이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumElementAfterDecreasingAndRearranging.java){:target="_blank"}에서 확인 가능합니다.