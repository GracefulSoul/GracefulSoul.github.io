---
title: "Leetcode Java Construct the Lexicographically Largest Valid Sequence"
excerpt: "Leetcode - 'Construct the Lexicographically Largest Valid Sequence' 문제 Java 풀이"
last_modified_at: 2025-02-16T16:00:00
header:
  image: /assets/images/leetcode/find-the-punishment-number-of-an-integer.png
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
[Link](https://leetcode.com/problems/find-the-punishment-number-of-an-integer/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] constructDistancedSequence(int n) {
    int[] result = new int[(n * 2) - 1];
    boolean[] visited = new boolean[n + 1];
    this.backtrack(n, result, 0, visited);
    return result;
  }

  private boolean backtrack(int n, int[] result, int index, boolean[] visited) {
    if (index == result.length) {
      return true;
    } else if (result[index] != 0) {
      return this.backtrack(n, result, index + 1, visited);
    } else {
      for (int i = n; i >= 1; i--) {
        if (!visited[i]) {
          visited[i] = true;
          result[index] = i;
          if (i == 1) {
            if (this.backtrack(n, result, index + 1, visited)) {
              return true;
            }
          } else if (index + i < result.length && result[index + i] == 0) {
            result[index + i] = i;
            if (this.backtrack(n, result, index + 1, visited)) {
              return true;
            }
            result[index + i] = 0;
          }
          result[index] = 0;
          visited[i] = false;
        }
      }
      return false;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/construct-the-lexicographically-largest-valid-sequence/submissions/1544785866/){:target="_blank"}

# 설명
1. 정수 n을 이용하여 아래의 규칙을 만족하는 사전적으로 가장 큰 배열을 반환하는 문제이다.
- 정수 1은 한 번만 발생한다.
- 2와 n 사이의 값들은 두 번씩 발생한다.
- 2와 n 사이의 임의 값 i에 대해서 동일한 값과의 거리는 정확히 i이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과를 넣을 변수로, 조건에 해당하는 값의 크기인 $(n \times 2) - 1$ 크기의 정수 배열로 초기화한다.
- visited는 숫자 사용 여부를 저장할 변수로, $n + 1$ 크기의 정수 배열로 초기화한다.

3. 4번에서 정의한 backtrack(int n, int[] result, int index, boolean[] visited) 메서드에 n, result, 0, visited를 넣어 수행한다.

4. 배열의 역순으로 탐색하며 조건에 만족하는 배열을 완성하기 위한 backtrack(int n, int[] result, int index, boolean[] visited) 메서드를 정의한다.
- index가 result의 길이와 동일한 마지막 수행인 경우, true를 반환한다.
- result[index]의 값이 0이 아닌 값이 설정된 경우, index를 증가시켜 재귀 수행한 결과를 반환한다.
- 위의 모든 경우가 아니라면 i를 n부터 1 이상일 때 까지 감소시키며 visited[i]가 false인 경우만 아래를 반복한다.
  - visited[i]의 값을 true로 넣어주고, result[index]에 i를 넣어준다.
  - i가 1인 경우, index를 증가시켜 재귀 수행시킨 결과가 true인 경우 true를 반환한다.
  - i가 1이 아니면서 $index + i$가 result 길이보다 작고 result[$index + i$]의 값이 0인 값 설정이 안 된 경우, result[$index + i$]에 i를 넣고 index를 증가시켜 재귀 수행 시킨 결과가 true인 경우 true를 반환하고 result[$index + i$]에 다시 0을 넣어 초기화시켜준다.
  - result[index]에 0을 넣고, visited[i]에 false를 넣어 초기화시켜준다.

5. 수행이 완료되어 완성된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConstructTheLexicographicallyLargestValidSequence.java){:target="_blank"}에서 확인 가능합니다.