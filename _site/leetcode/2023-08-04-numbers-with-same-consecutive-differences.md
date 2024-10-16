---
title: "Leetcode Java Numbers With Same Consecutive Differences"
excerpt: "Leetcode Numbers With Same Consecutive Differences Java"
last_modified_at: 2023-08-04T19:20:00
header:
  image: /assets/images/leetcode/numbers-with-same-consecutive-differences.png
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
[Link](https://leetcode.com/problems/numbers-with-same-consecutive-differences){:target="_blank"}

# 코드
```java
class Solution {

  public int[] numsSameConsecDiff(int n, int k) {
    List<Integer> list = new ArrayList<>();
    for (int i = 1; i <= 9; i++) {
      this.dfs(list, i, 1, n, k);
    }
    int length = list.size();
    int[] result = new int[length];
    for (int i = 0; i < length; i++) {
      result[i] = list.get(i);
    }
    return result;
  }

  private void dfs(List<Integer> list, int item, int i, int n, int k) {
    if (i == n) {
      list.add(item);
    } else {
      int a = item % 10;
      if (k == 0) {
        this.dfs(list, (item * 10) + a, i + 1, n, k);
      } else {
        if ((a + k) <= 9) {
          this.dfs(list, (item * 10) + (a + k), i + 1, n, k);
        }
        if ((a - k) >= 0) {
          this.dfs(list, (item * 10) + (a - k), i + 1, n, k);
        }
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/numbers-with-same-consecutive-differences/submissions/1011953675/){:target="_blank"}

# 설명
1. n 길이의 숫자 중 앞뒤 자리가 k인 숫자들을 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- list는 해당 조건에 맞는 숫자들을 저장할 변수로, ArrayList로 초기화하고 3번에서 정의한 dfs(List<Integer> list, int item, int i, int n, int k) 메서드를 1부터 9까지 i를 증가시키며 수행한 결과를 넣어준다.
- length는 위에서 수행된 list의 길이를 저장한 변수이다.
- result는 결과를 저장할 변수로, length 길이의 정수 배열로 초기화하고 list의 결과를 그대로 넣어 주어진 문제의 결과로 반환한다.

3. DFS 방식으로 값을 탐색하기 위한 dfs(List<Integer> list, int item, int i, int n, int k) 메서드를 메서드를 정의한다.
- i가 n인 자릿수가 맞는 경우, list에 item을 넣어준다.
- 위의 경우가 아니라면 a에 item을 10으로 나눈 나머지를 넣어주고 아래를 수행한다.
  - k가 0인 차이가 없을 경우 item에 $(item \times 10) + a$와 i에 1을 증가시켜 재귀 호출을 수행한다.
  - 위의 경우가 아니고 $a + k$가 9 이하인 경우, item에 $(item \tiems 10) + (a + k)$와 i에 1을 증가시켜 재귀 호출을 수행한다.
  - 위의 경우가 아니고 $a + k$가 0 이상인 경우, item에 $(item \tiems 10) + (a - k)$와 i에 1을 증가시켜 재귀 호출을 수행한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumbersWithSameConsecutiveDifferences.java){:target="_blank"}에서 확인 가능합니다.