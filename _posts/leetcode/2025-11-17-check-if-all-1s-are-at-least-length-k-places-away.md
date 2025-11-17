---
title: "Leetcode Java Check If All 1's Are at Least Length K Places Away"
excerpt: "Leetcode - 'Check If All 1's Are at Least Length K Places Away' 문제 Java 풀이"
last_modified_at: 2025-11-17T20:00:00
header:
  image: /assets/images/leetcode/check-if-all-1s-are-at-least-length-k-places-away.png
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
[Link](https://leetcode.com/problems/check-if-all-1s-are-at-least-length-k-places-away/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean kLengthApart(int[] nums, int k) {
    for (int i = -1, j = 0; j < nums.length; j++)
      if (nums[j] == 1) {
        if (i != -1 && j - i - 1 < k) {
          return false;
        }
        i = j;
      }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/check-if-all-1s-are-at-least-length-k-places-away/submissions/1832187904/){:target="_blank"}

# 설명
1. 정수 배열 nums 내 '1' 사이의 '0'의 갯수가 최소 k개가 되는지 검증하는 문제이다.

2. 1의 시작 지점을 저장할 i는 -1로 정의하고, 이후 탐색을 진행할 j는 0에서 nums의 길이 미만까지 j를 증가시키며 아래를 반복한다.
- nums[j]의 값이 1인 경우, 아래를 수행한다.
  - i가 -1이 아닌 초기 지점이 아니면서 $j - i - 1$의 값인 0의 갯수가 k개 미만인 조건을 만족하지 않는 경우, false를 주어진 문제의 결과로 반환한다.
  - i에 j를 넣어 현재 위치를 저장해준다.

3. 반복이 완료되면 nums가 조건을 만족하는 숫자로 구성되었으므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CheckIfAll1sAreAtLeastLengthKPlacesAway.java){:target="_blank"}에서 확인 가능합니다.