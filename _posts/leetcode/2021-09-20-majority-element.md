---
title: "Leetcode Java Majority Element"
excerpt: "Leetcode Majority Element Java 풀이"
last_modified_at: 2021-09-20T08:30:00
header:
  image: /assets/images/leetcode/majority-element.png
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
[Link](https://leetcode.com/problems/majority-element/){:target="_blank"}

# 코드
```java
class Solution {

  public int majorityElement(int[] nums) {
    int result = 0;
    int count = 0;
    for (int num : nums) {
      if (count == 0) {
        result = num;
      }
      if (num != result) {
        count--;
      } else {
        count++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/557737861/){:target="_blank"}

# 설명
1. 주어진 배열 nums에 속한 정수 중 과반수 이상 들어있는 값을 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 과반수 이상 존재하는 값을 저장하기 위한 변수이다.
- count는 과반수 이상이 존재하는지를 검증하기 위한 변수이다.

3. 주어진 배열 nums를 반복하여 과반수 이상 존재하는 값을 변수 result에 넣는다.
- count가 0일 경우 처음 시작이거나 타 값이 더 많이 존재하는 경우이므로, result에 num을 넣어준다.
- 반복되는 정수 num이 result와 같지 않으면 count를 감소시키고, 같으면 count를 증가시킨다.

4. 반복이 완료되면 과반수 이상 존재하는 정수를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MajorityElement.java){:target="_blank"}에서 확인 가능합니다.