---
title: "Leetcode Java Count Elements With Maximum Frequency"
excerpt: "Leetcode Easy - 'Count Elements With Maximum Frequency' 문제 Java 풀이"
last_modified_at: 2024-03-08T19:30:00
header:
  image: /assets/images/leetcode/count-elements-with-maximum-frequency.png
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
[Link](https://leetcode.com/problems/count-elements-with-maximum-frequency){:target="_blank"}

# 코드
```java
class Solution {

  public int maxFrequencyElements(int[] nums) {
    int[] count = new int[101];
    int max = 0;
    for (int num : nums) {
      count[num]++;
      if (count[num] > max) {
        max = count[num];
      }
    }
    int result = 0;
    for (int num : nums) {
      if (max == count[num]) {
        result += count[num]--;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-elements-with-maximum-frequency/submissions/1197528066/){:target="_blank"}

# 설명
1. nums 내 가장 많이 존재하는 값들의 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 nums 내 숫자들의 갯수를 계산할 변수로, 발생 가능한 최댓값의 크기보다 1 큰 정수 배열로 초기화한다.
- max는 nums 내 가장 많이 존재하는 숫자의 갯수를 저장할 변수로, 0으로 초기화한다.

3. nums를 반복하여 count에 숫자들의 갯수를, max에 가장 많이 존재하는 숫자의 갯수를 저장해준다.

4. result에 최대 발생한 갯수를 누계하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountElementsWithMaximumFrequency.java){:target="_blank"}에서 확인 가능합니다.