---
title: "Leetcode Java Russian Doll Envelopes"
excerpt: "Leetcode Russian Doll Envelopes Java 풀이"
last_modified_at: 2022-01-25T13:00:00
header:
  image: /assets/images/leetcode/russian-doll-envelopes.png
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
[Link](https://leetcode.com/problems/russian-doll-envelopes/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxEnvelopes(int[][] envelopes) {
    int dp[] = new int[envelopes.length];
    int count = 0;
    Arrays.sort(envelopes, (e1, e2) -> e1[0] == e2[0] ? e2[1] - e1[1] : e1[0] - e2[0]);
    for (int[] envelope : envelopes) {
      int index = Arrays.binarySearch(dp, 0, count, envelope[1]);
      if (index < 0) {
        index = -(index + 1);
      }
      dp[index] = envelope[1];
      if (index == count) {
        count++;
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/627203714/){:target="_blank"}

# 설명
1. 주어진 배열 envelopes는 봉투의 너비와 높이를 나타내는 정수의 2차원 배열로, 러시아 인형과 같이 작은 봉투를 큰 봉투에 순차적으로 넣을 수 봉투의 최대 개수를 구하는 문제이다.
- envelopes[i] = [width, height]
- 봉투를 회전시킬 수 없다.

2. 문제 풀이에 필요한 변수를 정의한다.
- dp는 envelopse를 이용하여 값을 순차적으로 넣어 활용하기 위한 배열로, envelopes.length의 크기로 초기화한다.
- count는 봉투를 러시아 인형같이 사용할 수 있는 최대 개수를 저장할 변수로, 0으로 초기화한다.

3. envelopes를 아래의 조건으로 정렬한다.
- e1의 첫 번째 값과 e2의 첫 번째 같이 같으면 $e2[1] - e1[1]$의 결과로 정렬을 수행한다.
- 위의 경우가 아니면, $e1[0] - e2[0]$의 결과로 정렬을 수행한다.

4. envelopes를 반복하여 최대 개수를 count에 누적한다.
- index는 Arrays의 binarySearch 메소드를 활용하여 envelope의 두 번째 값의 위치를 이진 검색 수행한 위치 값을 넣어준다.
- index가 0보다 작은 경우, index에 $index + 1$을 음수로 전환한 값으로 넣어준다.
- dp의 index번째 값에 envelope의 두 번째 값을 넣어준다.
- index와 count가 동일한 경우, count를 증가시켜주고 반복을 계속 수행한다.

5. 반복이 완료되면 최대 개수를 저장한 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RussianDollEnvelopes.java){:target="_blank"}에서 확인 가능합니다.