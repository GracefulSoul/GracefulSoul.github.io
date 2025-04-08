---
title: "Leetcode Java Minimum Number of Operations to Make Elements in Array Distinct"
excerpt: "Leetcode - 'Minimum Number of Operations to Make Elements in Array Distinct' 문제 Java 풀이"
last_modified_at: 2025-04-08T20:00:00
header:
  image: /assets/images/leetcode/minimum-number-of-operations-to-make-elements-in-array-distinct.png
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
[Link](https://leetcode.com/problems/minimum-number-of-operations-to-make-elements-in-array-distinct/){:target="_blank"}

# 코드
```java
class Solution {

  public int minimumOperations(int[] nums) {
    boolean[] seen = new boolean[101];
    for (int i = nums.length - 1; i >= 0; i--) {
      if (seen[nums[i]]) {
        return (i + 3) / 3;
      } else {
        seen[nums[i]] = true;
      }
    }
    return 0;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-number-of-operations-to-make-elements-in-array-distinct/submissions/1600531274/){:target="_blank"}

# 설명
1. 남은 배열 내 값이 고유한 값이 되도록 배열 시작의 세 값들을 계속 제거할 때, 제거 횟수를 구하는 문제이다.

2. seen은 동일한 값 발생 여부를 확인하기 위한 배열로, 최대 가능한 값보다 1 큰 101 크기의 부울 배열로 초기화한다.

3. nums의 길이보다 1 낮은 값부터 0 이상까지 i를 증가시키며 아래를 반복한다.
- seen[nums[i]]의 값이 true이면, 남은 값들을 제거하는 최소 횟수인 $\frac{i + 3}{3}$의 몫을 주어진 문제의 결과로 반환한다.
- seen[nums[i]]의 값이 false이면, 본 값을 체크하기 위해서 seen의 해당 위치에 true를 넣어준다.

4. 반복이 완료되면 0을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumNumberOfOperationsToMakeElementsInArrayDistinct.java){:target="_blank"}에서 확인 가능합니다.