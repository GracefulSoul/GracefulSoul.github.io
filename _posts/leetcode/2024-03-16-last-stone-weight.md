---
title: "Leetcode Java Last Stone Weight"
excerpt: "Leetcode Easy - 'Last Stone Weight' 문제 Java 풀이"
last_modified_at: 2024-03-16T11:10:00
header:
  image: /assets/images/leetcode/last-stone-weight.png
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
[Link](https://leetcode.com/problems/last-stone-weight){:target="_blank"}

# 코드
```java
class Solution {

  public int lastStoneWeight(int[] stones) {
    Arrays.sort(stones);
    for (int i = stones.length - 1, j = i - 1; j >= 0;) {
      if (stones[j] == stones[i]) {
        stones[i] = 0;
        stones[j] = 0;
      } else if (stones[j] > stones[i]) {
        stones[j] = stones[j] - stones[i];
        stones[i] = 0;
      } else {
        stones[j] = stones[i] - stones[j];
        stones[i] = 0;
      }
      Arrays.sort(stones, 0, i);
      i--;
      j--;
    }
    return stones[0];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/last-stone-weight/submissions/1204854088/){:target="_blank"}

# 설명
1. 돌의 무게를 가진 stones를 이용하여 아래의 규칙을 만족하는 결과를 반환하는 문제이다.
- 가장 무거운 두 돌의 돌맹이의 무게가 같으면 두 돌 모두 파괴된다.
- 가장 무거운 두 돌의 돌맹이의 무게가 다르면 두 돌의 차이를 남긴다.
- 마지막 남은 돌이 없으면 0을 반환한다.

2. stones의 값들을 오름차순으로 정렬한다.

3. i는 $stones.length - 1$로, j는 $i - 1$로 초기화하여 j가 0보다 클 때 까지 아래를 반복한다.
- stones의 i번째 돌과 j번째 돌의 무게가 동일하면 0으로 둘 모두 0으로 바꾼다.
- 위의 경우가 아니라 어느 한 쪽 돌의 무게가 크다면, 큰 돌의 자리에 두 돌의 차잇값을 넣어준다.
- stones의 처음부터 j까지 돌들의 무게를 오름차순 정렬하고 i와 j를 감소한다.

4. 수행이 완료되면 stones의 첫 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LastStoneWeight.java){:target="_blank"}에서 확인 가능합니다.