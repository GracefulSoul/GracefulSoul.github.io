---
title: "Leetcode Java Global and Local Inversions"
excerpt: "Leetcode Global and Local Inversions Java"
last_modified_at: 2022-12-21T14:50:00
header:
  image: /assets/images/leetcode/global-and-local-inversions.png
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
[Link](https://leetcode.com/problems/global-and-local-inversions){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isIdealPermutation(int[] nums) {
    int max = 0;
    for (int idx = 0; idx < nums.length - 2; idx++) {
      max = Math.max(max, nums[idx]);
      if (max > nums[idx + 2]) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/global-and-local-inversions/submissions/863035832/){:target="_blank"}

# 설명
1. [0, n - 1] 범위의 값을 담은 num를 이용하여 아래의 규칙대로 수행되는 Global Inversions의 수와 Local Inversions의 수가 동일한지 검증하는 문제이다.
- Global Inversions의 수는 아래의 조건을 만족하는 (i, j)의 다른 쌍의 수이다.
  - 0 <= i < j < n
  - nums[i] > nums[j]
- Local Inversions의 수는 아래의 조건을 만족하는 인덱스 i의 수이다.
  - 0 <= i < n - 1
  - nums[i] > nums[i + 1]

2. max는 가장 큰 값을 저장할 변수로, 0으로 초기화한다.

3. 0부터 nums의 길이보다 2 작은 크기 미만으로 idx를 증가시키며 아래를 반복한다.
- max에 max와 nums의 idx번째 값 중 큰 값을 저장한다.
- max와 nums의 $idx + 2$번째 값 중 max가 큰 경우, 두 Inversions의 수가 다르므로 false를 반환한다.
  - 모든 Local Inversions는 Global Inversions를 만족하므로, 두 수가 같다는 의미는 Global Inversions 또한 Local Inversions를 만족한다는 의미이다.
  - 그렇기 때문에 $i + 2 <= j$일때 nums[i] > nums[j]를 찾을 수 없다는 의미가 된다.
  - 즉, nums의 idx번째 값까지의 가장 큰 값이 $idx + 2$번째 값보다 크게되는 경우, 두 Inversions의 수가 다르게된다.

4. 반복이 완료되면 두 Inversions의 수가 같으므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/GlobalAndLocalInversions.java){:target="_blank"}에서 확인 가능합니다.