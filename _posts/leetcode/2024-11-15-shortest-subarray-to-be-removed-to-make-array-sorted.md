---
title: "Leetcode Java Shortest Subarray to be Removed to Make Array Sorted"
excerpt: "Leetcode - 'Shortest Subarray to be Removed to Make Array Sorted' 문제 Java 풀이"
last_modified_at: 2024-11-15T18:00:00
header:
  image: /assets/images/leetcode/shortest-subarray-to-be-removed-to-make-array-sorted.png
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
[Link](https://leetcode.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted/){:target="_blank"}

# 코드
```java
class Solution {

  public int findLengthOfShortestSubarray(int[] arr) {
    int length = arr.length;
    int left = 0;
    int right = length - 1;
    while (left + 1 < length && arr[left] <= arr[left + 1]) {
      left++;
    }
    if (left == length - 1) {
      return 0;
    }
    while (0 < right && arr[right - 1] <= arr[right]) {
      right--;
    }
    int i = 0;
    int j = right;
    int result = Math.min(length - left - 1, right);
    while (i <= left && j < length) {
      if (arr[i] <= arr[j]) {
        result = Math.min(result, j - i - 1);
        i++;
      } else {
        j++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted/submissions/1453355067/){:target="_blank"}

# 설명
1. arr 내 값들이 감소하지 않는 순서로 만들기 위해 삭제할 부분 문자열의 길이를 반환하는 문제이다.

2. 사전 범위를 계산하기 위한 변수를 정의한다.
- length는 arr의 길이를 저장한 변수이다.
- left와 right는 arr의 위치를 저장할 변수로, 시작 위치인 0과 종료 위치인 $length - 1$로 초기화한다.

3. $left + 1$이 length 미만이면서 arr[left]의 값이 arr[$left + 1$]의 값 이하인 감소하지 않는 순서를 만족할 때 까지 left를 증가시켜준다.

4. left가 $length - 1$인 마지막 위치인 경우 삭제할 숫자가 없으므로, 0을 주어진 문제의 결과로 반환한다.

5. right가 0 초과이면서 arr[$right - 1$]의 값이 arr[right]의 값 이하인 감소하지 않는 순서를 만족할 때 까지 right를 감소시켜준다.

6. arr에서 삭제할 부분 문자열의 길이를 확인하기 위한 변수를 정의한다.
- i와 j는 부분 문자열 삭제하기 위한 위치를 탐색할 변수로, 0과 right로 초기화한다.
- result는 결과를 저장할 변수로, $length - left - 1$과 right 중 작은 값을 넣어준다.

7. i는 left 이하이고 j는 length 이하일 때 까지 아래를 반복한다.
- arr[i]의 값이 arr[j] 이하인 경우 조건을 만족하므로, result에 result와 $j - i - 1$인 현재 부분 문자열 길이 중 작은 값을 넣어주고 i를 증가시켜준다.
- 위를 만족하지 않으면 arr[j]도 삭제해야하므로, j를 증가시켜준다.

8. 반복이 완료되면 삭제할 부분 문자열의 길이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShortestSubarrayToBeRemovedToMakeArraySorted.java){:target="_blank"}에서 확인 가능합니다.