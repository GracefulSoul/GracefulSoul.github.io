---
title: "Leetcode Java Advantage Shuffle"
excerpt: "Leetcode Advantage Shuffle Java"
last_modified_at: 2023-03-11T08:30:00
header:
  image: /assets/images/leetcode/advantage-shuffle.png
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
[Link](https://leetcode.com/problems/advantage-shuffle){:target="_blank"}

# 코드
```java
class Solution {

  public int[] advantageCount(int[] nums1, int[] nums2) {
    int length = nums1.length;
    Integer[] position = new Integer[length];
    for (int i = 0; i < length; i++) {
      position[i] = i;
    }
    int result[] = new int[length];
    Arrays.sort(position, (i, j) -> nums2[i] - nums2[j]);
    Arrays.sort(nums1);
    int low = 0;
    int high = length - 1;
    for (int i = length - 1; i >= 0; i--) {
      int index = position[i];
      if (nums2[index] < nums1[high]) {
        result[index] = nums1[high--];
      } else {
        result[index] = nums1[low++];
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/advantage-shuffle/submissions/912940359/){:target="_blank"}

# 설명
1. 길이가 같은 nums과 nums2를 이용하여 nums2의 장점을 최대화하는 nums1의 순열을 반환하는 문제이다.
- nums2의 장점은 nums1[i] > nums2[i]인 인덱스의 개수이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums1의 길이를 저장한 변수이다.
- position은 각 위치 별 위치 값을 저장할 변수로, 모든 자리에 자신의 위치 값을 넣어준다.
- result는 nums2의 장점을 최대화 하는 num1의 순열을 저장할 변수로, length 길이의 정수 배열로 초기화한다.

3. position은 result의 값 기준에 대한 위치 값을 오름차순으로 넣어주고, num1을 오름차순으로 정렬한다.

4. nums1의 값의 탐색에 사용할 low에 0을, high에 $length - 1$을 넣어 위치 변수를 초기화한다.

5. $length - 1$부터 0 이상까지 i를 감소시키며 아래를 반복한다.
- index에 position의 i번째 값을 꺼내 넣어준다.
- nums2의 index번째 값이 nums1의 high번째 값보다 작은 경우, result의 index번째 위치에 nums1의 high번째 값을 넣어주고 high를 감소시킨다.
- 위의 경우가 아니라면 result의 index번째 위치에 nums1의 low번째 값을 넣어주고 low를 증가시킨다.

6. 반복이 완료되면 결과를 저장한 nums2를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AdvantageShuffle.java){:target="_blank"}에서 확인 가능합니다.