---
title: "Leetcode Java Maximum Subarray Sum with One Deletion"
excerpt: "Leetcode Medium - 'Maximum Subarray Sum with One Deletion' 문제 Java 풀이"
last_modified_at: 2024-09-19T18:10:00
header:
  image: /assets/images/leetcode/maximum-subarray-sum-with-one-deletion.png
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
[Link](https://leetcode.com/problems/maximum-subarray-sum-with-one-deletion/){:target="_blank"}

# 코드
```java
class Solution {

  public int maximumSum(int[] arr) {
    int oneDeletion = 0;
    int noDeletion = arr[0];
    int result = arr[0];
    for (int i = 1; i < arr.length; i++) {
      oneDeletion = Math.max(oneDeletion + arr[i], noDeletion);
      noDeletion = Math.max(noDeletion + arr[i], arr[i]);
      result = Math.max(result, Math.max(oneDeletion, noDeletion));
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-subarray-sum-with-one-deletion/submissions/1395269536/){:target="_blank"}

# 설명
1. arr에서 연속된 값들로 이루어진 부분 배열에서 최대 하나의 값을 제거한 후 합이 가장 큰 값을 반환하는 문제이다.
- 단, 부분 배열은 하나의 값을 제거한 후에 비어있을 수 없다.

2. 문제 풀이에 핑료한 변수를 정의한다.
- oneDeletion은 한 값을 제거한 부분 배열의 합계를 계산할 변수로, 0으로 초기화한다.
- noDeletion은 값을 제거하지 않은 부분 배열의 합계를 계산할 변수로, arr[0] 값으로 초기화한다.
- result는 가능한 가장 큰 합계를 저장할 변수로, arr[0] 값으로 초기화한다.

3. 1부터 arr의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- oneDeletion에 아래의 두 값 중 큰 값을 넣어준다.
  - oneDeletion의 값에 arr[i]를 더한 누계한 값.
  - 현재 값을 포함하지 않은 noDeletion의 값.
- noDeletion에 아래의 두 값 중 큰 값을 넣어준다.
  - noDeletion의 값에 arr[i]를 더한 누계한 값.
  - 다시 연속된 값이 시작되는 경우인 arr[i]의 값.
- result에 result와 위의 각 경우인 oneDeletion과 noDeletion 중 큰 값을 넣어준다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumSubarraySumWithOneDeletion.java){:target="_blank"}에서 확인 가능합니다.