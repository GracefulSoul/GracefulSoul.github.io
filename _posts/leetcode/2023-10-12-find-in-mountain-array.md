---
title: "Leetcode Java Find in Mountain Array"
excerpt: "Leetcode Find in Mountain Array Java"
last_modified_at: 2023-10-12T19:50:00
header:
  image: /assets/images/leetcode/find-in-mountain-array.png
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
[Link](https://leetcode.com/problems/find-in-mountain-array){:target="_blank"}

# 코드
```java
/**
 * // This is MountainArray's API interface.
 * // You should not implement it, or speculate about its implementation
 * interface MountainArray {
 *     public int get(int index) {}
 *     public int length() {}
 * }
 */
 
class Solution {

  public int findInMountainArray(int target, MountainArray mountainArr) {
    int length = mountainArr.length();
    int peak = 0;
    for (int left = 0, right = length - 1; left < right;) {
      int mid = (left + right) / 2;
      if (mountainArr.get(mid) < mountainArr.get(mid + 1)) {
        left = peak = mid + 1;
      } else {
        right = mid;
      }
    }
    for (int left = 0, right = peak; left <= right;) {
      int mid = (left + right) / 2;
      int high = mountainArr.get(mid);
      if (high == target) {
        return mid;
      } else if (high > target) {
        right = mid - 1;
      } else {
        left = mid + 1;
      }
    }
    for (int left = peak, right = length - 1; left <= right;) {
      int mid = (left + right) / 2;
      int high = mountainArr.get(mid);
      if (high == target) {
        return mid;
      } else if (high < target) {
        right = mid - 1;
      } else {
        left = mid + 1;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-in-mountain-array/submissions/1073389911/){:target="_blank"}

# 설명
1. MountainArray를 이용하여 target에 해당하는 최소 위치를 반환하는 문제이다.
- 단, target에 해당하는 높이가 MountainArray에 존재하지 않으면 -1을 주어진 문제의 결과로 반환한다.
- MountainArray는 최소 3개 이상의 정수로 이루어져 있으며, 산꼭대기를 기준으로 좌측과 우측의 높이는 계속 감소한다.
- MountainArray의 length() 메서드는 산의 길이를 반환한다.
- MountainArray의 get(int index) 메서드는 index번째 위치에서 산의 높이를 반환하며, 100번 이상 호출하는 경우 오답으로 취급한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 mountainArr의 length() 메서드를 호출하여 길이를 저장한 변수이다.
- peak는 산꼭대기를 저장할 변수로, 0으로 초기화한다.

3. left는 0, right는 $length - 1$로 초기화하고 left가 right 미만까지 아래를 반복하여 산꼭대기 위치를 peak에 넣어준다.
- mid는 중앙값을 저장할 변수로, $\frac{left + right}{2}$로 초기화한다.
- mountainArr의 mid번째 높이가 $mid + 1$보다 작은 경우, left와 peak에 $mid + 1$을 넣어 하한 위치를 증가시킨다.
- 위의 경우가 아니라면, right에 mid를 넣어 상한 위치를 감소시킨다.

4. left는 0, right는 peak로 초기화하고 left가 right 이하일 때 까지 아래를 반복하여 산의 좌측 능선에서 target에 해당하는 위치를 탐색한다.
- mid는 중앙값을 저장할 변수로, $\frac{left + right}{2}$로 초기화한다.
- high는 mountainArr의 mid번째 높이를 가져와 넣어준다.
- high가 target과 동일한 경우, 가장 작은 좌측 능선에 대한 위치이므로 mid를 주어진 문제의 결과로 반환한다.
- high가 target보다 큰 경우, $mid - 1$을 넣어 상한 위치를 감소시킨다.
- 위의 모든 경우가 아닌 경우, left에 $mid + 1$을 넣어 하한 위치를 증가시킨다.

5. 위에서 존재하지 않는다면 left는 peak, right는 $length - 1$로 초기화하고 left가 right 이하일 때 까지 아래를 반복하여 산의 우측 능선에서 target에 해당하는 위치를 탐색한다.
- mid는 중앙값을 저장할 변수로, $\frac{left + right}{2}$로 초기화한다.
- high는 mountainArr의 mid번째 높이를 가져와 넣어준다.
- high가 target과 동일한 경우, 가장 작은 좌측 능선에 대한 위치이므로 mid를 주어진 문제의 결과로 반환한다.
- high가 target보다 큰 경우, $mid - 1$을 넣어 상한 위치를 감소시킨다.
- 위의 모든 경우가 아닌 경우, left에 $mid + 1$을 넣어 하한 위치를 증가시킨다.

6. 모든 반복이 완료되면 mountainArr의 각 위치 별 높이에서 target에 해당하는 높이가 존재하지 않으므로, -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindInMountainArray.java){:target="_blank"}에서 확인 가능합니다.