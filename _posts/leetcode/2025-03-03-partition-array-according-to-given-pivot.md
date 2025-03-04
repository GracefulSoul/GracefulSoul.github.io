---
title: "Leetcode Java Partition Array According to Given Pivot"
excerpt: "Leetcode - 'Partition Array According to Given Pivot' 문제 Java 풀이"
last_modified_at: 2025-03-03T22:40:00
header:
  image: /assets/images/leetcode/partition-array-according-to-given-pivot.png
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
[Link](https://leetcode.com/problems/partition-array-according-to-given-pivot/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] pivotArray(int[] nums, int pivot) {
    int length = nums.length;
    int[] result = new int[length];
    int i = 0;
    int j = 0;
    int k = 0;
    for (int num : nums) {
      if (num <= pivot) {
        k++;
        if (num < pivot) {
          j++;
        }
      }
    }
    for (int num : nums) {
      if (num < pivot) {
        result[i++] = num;
      } else if (num > pivot) {
        result[k++] = num;
      } else {
        result[j++] = num;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/partition-array-according-to-given-pivot/submissions/1560870779/){:target="_blank"}

# 설명
1. nums 내 값들을 pivot 기준으로 정렬하는 문제이다.
- 임의 i 위치에서 nums[i]의 값이 pivot 값 초과인 경우, nums의 우측으로 값을 이동한다.
- 임의 i 위치에서 nums[i]의 값이 pivot 값과 동일한 경우, pivot 값 미만인 값과 초과인 값 사이에 위치시킨다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- result는 조건에 만족한 값들을 정렬하여 저장할 변수로, length 길이의 정수 배열로 초기화한다.
- i, j, k는 pivot 값 미만, 동일, 초과의 값들을 저장할 위치 변수로, 모두 0으로 초기화한다.

3. nums의 값들을 순차적으로 num에 넣어, 아래를 수행한다.
- num이 pivot 미만이면 j만 증가시키고, pivot 이하이면 k도 증가시킨다.

4. 다시 nums의 값들을 순차적으로 num에 넣어, 아래를 수행한다.
- num이 pivot 값 미만인 경우, result[i] 위치에 num을 넣고 i를 증가시킨다.
- num이 pivot 값 초과인 경우, result[k] 위치에 num을 넣고 k를 증가시킨다.
- num이 pivot 값과 동일한 경우, result[j] 위치에 num을 넣고 j를 증가시킨다.

5. 반복이 완료되면 정렬된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PartitionArrayAccordingToGivenPivot.java){:target="_blank"}에서 확인 가능합니다.