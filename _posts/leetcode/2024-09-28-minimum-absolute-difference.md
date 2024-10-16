---
title: "Leetcode Java Minimum Absolute Difference"
excerpt: "Leetcode Minimum Absolute Difference Java"
last_modified_at: 2024-09-28T09:10:00
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
    List<List<Integer>> result = new ArrayList<>();
    int min = Integer.MAX_VALUE;
    Arrays.sort(arr);
    for (int i = 1; i < arr.length; i++) {
      int diff = arr[i] - arr[i - 1];
      if (diff < min) {
        min = diff;
        result.clear();
      }
      if (diff == min) {
        result.add(Arrays.asList(arr[i - 1], arr[i]));
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-absolute-difference/submissions/1404415550/){:target="_blank"}

# 설명
1. arr 내 값들의 최소 차잇값에 대한 값들을 한 쌍씩 묶어서 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과를 저장할 변수로, ArrayList로 초기화한다.
- min은 최소 차잇값을 저장할 변수로, 정수의 최댓값으로 초기화한다.

3. arr을 오름차순 정렬 후 1부터 arr의 길이 미만까지 i를 증가시키며 아래를 수행한다.
- diff에 arr[i]와 arr[$i - 1$]의 차잇값을 저장해준다.
- diff가 min보다 작은 경우, min에 diff 넣은 후 result를 초기화시켜준다.
- diff와 min이 동일한 최소 차잇값인 경우, result에 arr[$i - 1$]과 arr[i]를 한 쌍으로 넣어준다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumAbsoluteDifference.java){:target="_blank"}에서 확인 가능합니다.