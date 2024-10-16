---
title: "Leetcode Java Bitwise ORs of Subarrays"
excerpt: "Leetcode Bitwise ORs of Subarrays Java"
last_modified_at: 2023-04-11T19:45:00
header:
  image: /assets/images/leetcode/bitwise-ors-of-subarrays.png
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
[Link](https://leetcode.com/problems/bitwise-ors-of-subarrays){:target="_blank"}

# 코드
```java
class Solution {

  public int subarrayBitwiseORs(int[] arr) {
    Set<Integer> result = new HashSet<>();
    for (int i = 0; i < arr.length; i++) {
      result.add(arr[i]);
      for (int j = i - 1; j >= 0; j--) {
        int curr = arr[i] | arr[j];
        if (curr == arr[j]) {
          break;
        }
        arr[j] = curr;
        result.add(arr[j]);
      }
    }
    return result.size();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/bitwise-ors-of-subarrays/submissions/931841131/){:target="_blank"}

# 설명
1. arr을 이용하여 만들 수 있는 부분 배열들의 모든 값을 이용해 OR 비트 연산을 수행한 결과의 중복되지 않은 값의 수를 구하는 문제이다.

2. result는 결과를 넣을 변수로, 중복을 제거하고 넣을 HashSet으로 초기화한다.

3. 0부터 arr의 길이 미만까지 i를 증가시키며 아래를 수행한다.
- result에 i의 값을 추가하고, $i - 1$부터 0 이상까지 j를 감소시키며 아래를 검증한다.
  - curr에 arr[i]의 값과 arr[j]의 값의 OR 비트 연산의 결과를 넣어준다.
  - curr과 arr[j]의 값이 동일하면 결과는 arr[j]의 값에 수렴하므로, 반복을 중단한다.
  - arr[j]의 위치에 curr을 넣고, result에 해당 값을 넣어준다.

4. 반복이 완료되면 고유 값들만 저장된 result의 크기를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BitwiseORsOfSubarrays.java){:target="_blank"}에서 확인 가능합니다.