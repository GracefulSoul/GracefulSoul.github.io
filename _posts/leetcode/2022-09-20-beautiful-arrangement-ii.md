---
title: "Leetcode Java Beautiful Arrangement II"
excerpt: "Leetcode Beautiful Arrangement II Java"
last_modified_at: 2022-09-20T19:50:00
header:
  image: /assets/images/leetcode/beautiful-arrangement-ii.png
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
[Link](https://leetcode.com/problems/beautiful-arrangement-ii){:target="_blank"}

# 코드
```java
class Solution {

  public int[] constructArray(int n, int k) {
    int[] result = new int[n];
    int left = 1;
    int right = n;
    for (int idx = 0; idx < n; idx++) {
      result[idx] = k % 2 != 0 ? left++ : right--;
      if (k > 1) {
        k--;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/804396606/){:target="_blank"}

# 설명
1. 1부터 n까지 아래의 조건을 만족하는 양의 정수가 k개가 되는 조합을 배열로 만드는 문제이다.
- 문제의 결과인 answer = [a1, a2, a3, ... , an]일 때, [\|a1 - a2\|, \|a2 - a3\|, \|a3 - a4\|, ... , \|an-1 - an\|]의 결과의 중복되지 않은 양의 정수는 k개가 된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 1부터 n까지 숫자를 중복되지 않은 k개의 결과가 되는 순서의 조합을 저장할 배열로, n의 크기로 초기화한다.
- left와 right는 해당 숫자를 순차적으로 넣기 위한 위치를 넣을 변수로, 1과 n으로 초기화한다.

3. 0부터 n 미만까지 idx를 증가시키며 아래를 수행한다.
- k가 홀수인 경우, left를 증가하여 이전 값보다 1 큰 값을 result의 idx번째 위치에 넣어준다.
- k가 짝수인 경우, right를 감소하여 이전 값과 차이가 가장 큰 값을 result의 idx번째 위치에 넣어준다.
- k가 1보다 큰 경우, 값의 차이가 되는 숫자를 더 만들어야 하므로 k를 감소시켜 1이 될 때 까지 반복한다.

4. 반복이 완료되면 주어진 문제의 결과로 result를 넣어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BeautifulArrangementII.java){:target="_blank"}에서 확인 가능합니다.