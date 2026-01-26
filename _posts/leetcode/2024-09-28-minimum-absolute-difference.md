---
title: "Leetcode Java Minimum Absolute Difference"
excerpt: "Leetcode Easy - 'Minimum Absolute Difference' 문제 Java 풀이"
last_modified_at: 2026-01-26T19:15:00
header:
  image: /assets/images/leetcode/minimum-absolute-difference.png
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
[Link](https://leetcode.com/problems/minimum-absolute-difference/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> minimumAbsDifference(int[] arr) {
    Arrays.sort(arr);
    int min = Integer.MAX_VALUE;
    for (int i = 1; i < arr.length; i++) {
      min = Math.min(min, arr[i] - arr[i - 1]);
    }
    List<List<Integer>> result = new ArrayList<>();
    for (int i = 1; i < arr.length; i++) {
      int diff = arr[i] - arr[i - 1];
      if (min == diff) {
        result.add(Arrays.asList(arr[i - 1], arr[i]));
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-absolute-difference/submissions/1897423404/){:target="_blank"}

# 설명
1. arr 내 값들의 최소 차잇값에 대한 값들을 한 쌍씩 묶어서 반환하는 문제이다.

2. arr의 값들을 오름차순으로 정렬해준다.

3. 문제 풀이에 필요한 변수를 정의한다.
- min은 최소 차잇값을 저장하기 위한 변수로, 두 값의 차잇값이 최소인 값을 넣어준다.
- result는 결과를 저장하기 위한 변수로, ArrayList로 초기화한다.

4. 1부터 arr의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- diff는 $arr[i] - arr[i - 1]$인 인접한 두 값의 차잇값을 저장한다.
- min과 diff가 동일한 최소 차잇값을 만족하는 경우, result에 arr[$i - 1$]의 값과 arr[i]의 값을 쌍으로 넣어준다.

5. 반복이 완료되면 주어진 조건을 만족하는 결과만 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumAbsoluteDifference.java){:target="_blank"}에서 확인 가능합니다.