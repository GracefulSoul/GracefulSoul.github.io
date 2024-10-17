---
title: "Leetcode Java Contains Duplicate"
excerpt: "Leetcode - 'Contains Duplicate' 문제 Java 풀이"
last_modified_at: 2021-10-22T12:00:00
header:
  image: /assets/images/leetcode/contains-duplicate.png
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
[Link](https://leetcode.com/problems/contains-duplicate/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean containsDuplicate(int[] nums) {
    Set<Integer> set = new HashSet<>();
    for (int num : nums) {
      if (!set.add(num)) {
        return true;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/575188268/){:target="_blank"}

# 설명
1. 주어진 배열 nums 중 중복된 값이 있는지 검증하는 문제이다.

2. Set은 중복을 배제한 값을 저장하는 컬렉션으로, 주어진 문제를 검증하기 위해 변수 set을 정의한다.

3. nums를 반복하여 주어진 nums 중 중복된 값이 있는지 검증한다.
- set에 nums의 값들을 넣을 때 중복된 값이 있으면 true를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 중복된 값이 없으므로 false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ContainsDuplicate.java){:target="_blank"}에서 확인 가능합니다.