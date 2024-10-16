---
title: "Leetcode Java Trapping Rain Water"
excerpt: "Leetcode Trapping Rain Water Java 풀이"
last_modified_at: 2021-05-23T15:50:00
header:
  image: /assets/images/leetcode/trapping-rain-water.png
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
[Link](https://leetcode.com/problems/trapping-rain-water/){:target="_blank"}

# 코드
```java
class Solution {

  public int trap(int[] height) {
    int result = 0;
    if (height == null || height.length == 0) {
      return result;
    }
      int left = 0;
      int right = height.length - 1;
    int leftMax = -1;
    int rightMax = -1;
    while (left < right) {
        leftMax = Math.max(leftMax, height[left]);
        rightMax = Math.max(rightMax, height[right]);
        if (leftMax < rightMax) {
          result += leftMax - height[left];
          left++;
        } else {
          result += rightMax - height[right];
          right--;
        }
      }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/497010956/){:target="_blank"}

# 설명
1. 주어진 배열 height를 이용하여 비를 최대로 담을 수 있는 양을 구하는 문제이다.

2. 반복을 통해서 비를 담을 수 있는 최대 양을 저장하는 result를 정의한다.

3. 주어진 배열이 없거나, 크기가 0인 경우(주어진 문제의 배열 최소 사이즈는 0이므로) result를 주어진 문제의 결과로 반환한다.

4. 문제 풀이에 사용될 변수들을 선언한다.
- 탐색의 좌측 pointer인 left를 0으로 정의한다.
- 탐색의 우측 pointer인 right를 $height - 1$로 정의한다.
- 좌측의 최대 높이인 leftMax를 -1로 정의한다(height의 최소 높이는 0이다).
- 우측의 최대 높이인 rightMax를 -1로 정의한다(height의 최소 높이는 0이다).

5. right가 left보다 클 때까지 반복하여 비를 담을 수 있는 최대 양을 구한다.
- leftMax와 height[left] 값 중 큰 값을 leftMax에 주입하고, rightMax 또한 rightMax와 height[right] 값 중 큰 값을 reightMax에 주입한다.
- 만일 leftMax가 작은 경우, result에 $leftMax - height[left]$ 값을 추가하고 left 값을 증가시키고 반복을 계속한다.
- 만일 rightMax가 작은 경우, result에 $rifght - heigth[right]$ 값을 추가하고 right 값을 감소시키고 반복을 계속한다.

6. 반복이 끝나면 비를 담을 수 있는 최대 양을 저장한 result를 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TrappingRainWater.java){:target="_blank"}에서 확인 가능합니다.