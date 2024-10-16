---
title: "Leetcode Java Find Missing Observations"
excerpt: "Leetcode Find Missing Observations Java"
last_modified_at: 2024-09-05T19:40:00
header:
  image: /assets/images/leetcode/find-missing-observations.png
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
[Link](https://leetcode.com/problems/find-missing-observations/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] missingRolls(int[] rolls, int mean, int n) {
    int sum = 0;
    for (int roll : rolls) {
      sum += roll;
    }
    int less = (mean * (n + rolls.length)) - sum;
    if (less < n || (6 * n) < less) {
      return new int[0];
    } else {
      int quotient = less / n;
      int remainder = less % n;
      int[] result = new int[n];
      Arrays.fill(result, quotient);
      for (int i = 0; i < remainder; i++) {
        result[i] = quotient + 1;
      }
      for (int i = remainder; i < n; i++) {
        result[i] = quotient;
      }
      return result;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-missing-observations/submissions/1379816873/){:target="_blank"}

# 설명
1. 정육면체 주사위를 이용하여 이미 굴린 주사위의 값인 rolls을 중앙값인 mean을 만들기 위해서 주사위를 n번 굴린 결과의 조합을 찾는 문제이다.
- 단, 불가능하면 빈 배열을 주어진 문제의 결과로 반환한다.

2. less는 mean을 만들기 위해 부족한 값을 저장할 변수로, maen을 $n + rolls.length$인 중앙값이 되기 위한 값에 rolls의 값을 더한 부족한 값을 넣어준다.

3. less가 n보다 작거나 $6 \times n$인 추가로 굴린 값이 모두 6이어도 중앙값을 초과하는 경우, 빈 배열을 주어진 문제의 결과로 반환한다.

4. 3번의 경우가 아니라면 아래를 수행한다.
- 결과를 구하기 위한 변수를 정의한다.
  - quotient와 remainder는 부족한 less 값을 n으로 나눈 몫과 나머지를 저장한 변수이다.
  - result는 추가로 굴려서 나와야 하는 값을 저장할 변수로, n 크기의 정수 배열로 초기화하고 quotient를 모든 위치에 넣어준다.
- 0부터 remainder 미만까지 i를 증가시키며, result[i]에 $quotient + 1$의 값을 순차적으로 더해 부족한 값들을 채워준다.
- 나머지 위치에 quotient를 넣어주고 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindMissingObservations.java){:target="_blank"}에서 확인 가능합니다.