---
title: "Leetcode Java Merge Two 2D Arrays by Summing Values"
excerpt: "Leetcode - 'Merge Two 2D Arrays by Summing Values' 문제 Java 풀이"
last_modified_at: 2025-03-02T22:40:00
header:
  image: /assets/images/leetcode/merge-two-2d-arrays-by-summing-values.png
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
[Link](https://leetcode.com/problems/merge-two-2d-arrays-by-summing-values/){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] mergeArrays(int[][] nums1, int[][] nums2) {
    int nums1Length = nums1.length;
    int nums2Length = nums2.length;
    int i = 0;
    int j = 0;
    List<int[]> result = new ArrayList<>();
    while (i < nums1Length && j < nums2Length) {
      if (nums1[i][0] == nums2[j][0]) {
        result.add(new int[] { nums1[i][0], nums1[i++][1] + nums2[j++][1] });
      } else if (nums1[i][0] < nums2[j][0]) {
        result.add(nums1[i++]);
      } else {
        result.add(nums2[j++]);
      }
    }
    while (i < nums1Length) {
      result.add(nums1[i++]);
    }
    while (j < nums2Length) {
      result.add(nums2[j++]);
    }
    return result.toArray(new int[result.size()][]);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/merge-two-2d-arrays-by-summing-values/submissions/1560381340/){:target="_blank"}

# 설명
1. 아래의 규칙대로 구성된 nums1과 nums2 배열을 키 기준으로 값을 합쳐서 반환하는 문제이다.
- nums1과 nums2는 첫번째 값이 키이고, 두 번째 값으로 구성되어 있다.
- nums1과 nums2는 키 기준으로 오름차순 정렬되어 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- nums1Length와 nums2Length는 num1과 num2의 길이를 저장한 변수이다.
- i와 j는 num1과 num2 내 위치를 계산할 변수로, 0으로 초기화한다.
- result는 주어진 기준 내 키에 대한 값들의 합을 저장할 변수로, 합친 키의 갯수가 불분명하여 ArrayList로 초기화한다.

3. i가 nums1Length 미만이고, j가 nums2Length 미만일 때 까지 아래를 반복한다.
- nums1[i][0]의 값과 nums2[j][0]의 값이 동일한 경우, result에 nums1[i][0]의 값과 $nums1[i][1] + nums2[j][1]$ 값을 배열로 넣어주고 i와 j를 증가시킨다.
- nums1[i][0]의 값이 nums2[j][0]의 값보다 작은 경우, result에 nums1[i] 배열을 넣어주고 i를 증가시킨다.
- nums1[i][0]의 값이 nums2[j][0]의 값보다 큰 경우, result에 nums2[j] 배열을 넣어주고 j를 증가시킨다.

4. i가 nums1Length 미만일 때 까지 result에 nums1[i] 배열을 넣어주면서 i를 증가시켜 남은 배열을 넣어준다.

5. j가 nums1Length 미만일 때 까지 result에 nums2[j] 배열을 넣어주면서 i를 증가시켜 남은 배열을 넣어준다.

6. 반복이 완료되면 result를 해당 길이 크기의 정수 배열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MergeTwo2DArraysBySummingValues.java){:target="_blank"}에서 확인 가능합니다.