---
title: "Leetcode Java Peak Index in a Mountain Array"
excerpt: "Leetcode Peak Index in a Mountain Array Java"
last_modified_at: 2023-02-25T14:30:00
header:
  image: /assets/images/leetcode/peak-index-in-a-mountain-array.png
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
[Link](https://leetcode.com/problems/peak-index-in-a-mountain-array){:target="_blank"}

# 코드
```java
class Solution {

  public int peakIndexInMountainArray(int[] arr) {
    int left = 0;
    int right = arr.length - 1;
    while (left < right) {
      int mid = left + ((right - left) / 2);
      if (arr[mid] > arr[mid + 1]) {
        right = mid;
      } else {
        left = mid + 1;
      }
    }
    return left;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/peak-index-in-a-mountain-array/submissions/904504027/){:target="_blank"}

# 설명
1. 산의 높이가 저장된 arr을 이용하여 산꼭대기를 찾는 문제이다.
- 단, O(logN)의 시간 복잡성으로 문제를 풀어야 한다.
- 0 < i < $arr.length - 1$일 때, 아래를 만족한다.
  - arr[0] < arr[1] < ... < arr[i - 1] < arr[i] 
  - arr[i] > arr[$i + 1$] > ... > arr[$arr.length - 1$]
- 산꼭대기는 arr[0] < arr[1] < ... < arr[$i - 1$] < arr[i] > arr[$i + 1$] > ... > arr[$arr.length - 1$]를 만족한다.

2. left와 right는 좌측과 우측 기준으로 탐색할 변수로, 0과 $arr.length - 1$로 초기화한다.

3. left가 right 미만일 때 까지 아래를 수행한다.
- mid에 $left + \frac{right - left}{2}$를 넣어준다.
- arr의 mid번째 값이 $mid + 1$번째 값보다 큰 경우, 우측으로 탐색해야하므로 right에 mid를 넣어준다.
- 위를 만족하지 않으면, 좌측으로 탐색해야하므로 left에 $mid + 1$을 넣어준다.

4. 반복이 완료되면 산꼭대기의 위치가 저장된 left를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PeakIndexInAMountainArray.java){:target="_blank"}에서 확인 가능합니다.