---
title: "Leetcode Java Minimum Index of a Valid Split"
excerpt: "Leetcode - 'Minimum Index of a Valid Split' 문제 Java 풀이"
last_modified_at: 2025-03-27T20:20:00
header:
  image: /assets/images/leetcode/minimum-index-of-a-valid-split.png
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
[Link](https://leetcode.com/problems/minimum-index-of-a-valid-split/){:target="_blank"}

# 코드
```java
class Solution {

  public int minimumIndex(List<Integer> nums) {
    int size = nums.size();
    int max = Integer.MIN_VALUE;
    int count = 0;
    for (int num : nums) {
      if (count == 0) {
        max = num;
      }
      if (max == num) {
        count++;
      } else {
        count--;
      }
    }
    count = 0;
    for (int num : nums) {
      if (num == max) {
        count++;
      }
    }
    if (count <= (size - count) + 1) {
      return -1;
    }
    count = 0;
    for (int i = 0; i < size; i++) {
      if (nums.get(i) == max) {
        count++;
      } else {
        count--;
      }
      if (count == 1) {
        return i;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-index-of-a-valid-split/submissions/1588000960/){:target="_blank"}

# 설명
1. nums의 값들을 아래 조건을 만족하는 두 집단으로 분리할 수 있는 위치를 반환하는 문제이다.
- 0 <= i < $n - 1$을 만족하는 한 위치를 결정할 때, 두 집단은 절반 이상의 동일한 값을 가진다.

2. 문제 풀이에 필요한 변수를 정의한다.
- size는 nums의 크기를 저장한 변수이다.
- max는 최빈값의 갯수를 계산하기 위한 변수로, 정수의 최솟값을 넣어준다.
- count는 [Boyer–Moore majority vote algorithm](https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_majority_vote_algorithm){:target="_blank"}을 사용하여 계산하기 위한 변수로, 0으로 초기화한다.

3. nums의 값들을 순차적으로 반복하여 아래를 반복한다.
- count가 0인 경우, max에 num을 넣어준다.
- max와 num이 동일하면 count를 증가시키고, 그렇지 않으면 count를 감소시켜준다.

4. count를 0으로 초기화 한 후 nums 내 max에 해당하는 값의 갯수를 넣고 $(size - count) + 1$의 값이 count 이상인 발생 빈도가 과반 미만인 경우, -1을 주어진 문제의 결과로 반환한다.

5. count를 다시 0으로 초기화 후, 0부터 size 미만까지 i를 증가시키며 아래를 반복한다.
- nums의 i번째 값이 max이면 count를 증가시키고, 그렇지 않으면 count를 감소시켜준다.
- count가 1이 되는 과반 이상의 지점으로 분리 가능한 위치를 탐색한 경우, i를 주어진 문제의 결과로 반환한다.

6. 모든 수행이 완료되면 분리할 수 있는 위치를 탐색하지 못하였으므로, -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumIndexOfAValidSplit.java){:target="_blank"}에서 확인 가능합니다.