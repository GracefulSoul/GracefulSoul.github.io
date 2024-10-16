---
title: "Leetcode Java Majority Element II"
excerpt: "Leetcode Majority Element II Java 풀이"
last_modified_at: 2021-11-04T12:00:00
header:
  image: /assets/images/leetcode/majority-element-ii.png
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
[Link](https://leetcode.com/problems/majority-element-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> majorityElement(int[] nums) {
    int[] element = new int[2];
    int[] count = new int[2];
    for (int num : nums) {
      if (element[0] == num) {
        count[0]++;
      } else if (element[1] == num) {
        count[1]++;
      } else if (count[0] == 0) {
        element[0] = num;
        count[0]++;
      } else if (count[1] == 0) {
        element[1] = num;
        count[1]++;
      } else {
        count[0]--;
        count[1]--;
      }
    }
    List<Integer> result = new ArrayList<>();
    count[0] = count[1] = 0;
    for (int num : nums) {
      if (element[0] == num) {
        count[0]++;
      } else if (element[1] == num) {
        count[1]++;
      }
    }
    for (int idx = 0; idx < count.length; idx++) {
      if (count[idx] > nums.length / 3) {
        result.add(element[idx]);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/581794768/){:target="_blank"}

# 설명
1. 주어진 배열인 nums를 이용하여 nums의 크기를 n이라고 했을 때, $\frac{n}{3}$ 이상 발생한 숫자를 모두 찾아 반환하는 문제이다.
- [보이어-무어의 과반수 투표 알고리즘](https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_majority_vote_algorithm){:target="_blank"}을 기반으로 풀이를 한다.

2. 문제 풀이를 위한 변수를 정의한다.
- element는 많이 발생한 두 숫자를 넣어 결과의 후보군을 저장하기 위한 배열이다.
- count는 element의 동일한 index번째 숫자의 개수를 저장하기 위한 배열이다.

3. 주어진 배열인 nums를 반복하여 아래를 순차적으로 확인한다.
- element[0]의 값과 num이 동일하면, count[0]을 증가시키고 반복을 계속 수행한다.
- element[1]의 값과 num이 동일하면, count[1]을 증가시키고 반복을 계속 수행한다.
- count[0]이 0인 경우, element[0]에 num을 넣고 count[0]을 증가시키고 반복을 계속 수행한다.
- count[1]이 0인 경우, element[1]에 num을 넣고 count[1]을 증가시키고 반복을 계속 수행한다.
- 그 외의 경우, count[0]과 count[1]을 감소시킨다.

4. 결과를 넣을 컬렉션인 result를 정의하고, count 배열을 0으로 초기화한다.

5. nums를 다시 반복하여 element에 저장된 후보군들이 nums에 존재하는 개수를 계산한다.

6. 후보군을 저장한 element들의 count가 $\frac{nums.length}{3}$ 초과인지를 확인하여 result에 넣어준다.

7. 주어진 배열인 nums의 $\frac{n}{3}$ 이상 발생한 숫자들을 모두 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MajorityElementII.java){:target="_blank"}에서 확인 가능합니다.