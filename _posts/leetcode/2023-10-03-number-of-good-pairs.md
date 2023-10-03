---
title: "Leetcode Java Number of Good Pairs"
excerpt: "Leetcode Number of Good Pairs Java"
last_modified_at: 2023-10-03T10:05:00
header:
  image: /assets/images/leetcode/number-of-good-pairs.png
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
[Link](https://leetcode.com/problems/number-of-good-pairs){:target="_blank"}

# 코드
```java
class Solution {

  public int numIdenticalPairs(int[] nums) {
    int result = 0;
    int[] count = new int[101];
    for (int num : nums) {
      result += count[num]++;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-good-pairs/submissions/1065433628/){:target="_blank"}

# 설명
1. nums 배열 내 동일한 값의 위치를 짝을 지을 경우, 가능한 경우의 수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 경우의 수를 저장하기 위한 변수로, 0으로 초기화한다.
- count는 동일한 값 별로 갯수를 저장할 배열로, 값의 최댓값인 100보다 1 큰 101 크기의 정수 배열로 초기화한다.

3. nums의 모든 값을 반복하여 count의 해당 값을 증가시키고 result에 해당 값을 더해준다.
- n이란 값의 동일한 갯수가 증가할 경우, n!의 짝을 만들 수 있다.

4. 반복이 완료되면 겅우의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfGoodPairs.java){:target="_blank"}에서 확인 가능합니다.