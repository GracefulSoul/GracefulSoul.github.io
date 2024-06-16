---
title: "Leetcode Java Number of Equivalent Domino Pairs"
excerpt: "Leetcode Number of Equivalent Domino Pairs Java"
last_modified_at: 2024-06-16T12:50:00
header:
  image: /assets/images/leetcode/number-of-equivalent-domino-pairs.png
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
[Link](https://leetcode.com/problems/number-of-equivalent-domino-pairs/){:target="_blank"}

# 코드
```java
class Solution {

  public int numEquivDominoPairs(int[][] dominoes) {
    int[] count = new int[100];
    int result = 0;
    for (int[] domino : dominoes) {
      if (domino[0] < domino[1]) {
        result += count[domino[0] * 10 + domino[1]]++;
      } else {
        result += count[domino[1] * 10 + domino[0]]++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-equivalent-domino-pairs/submissions/1289707491/){:target="_blank"}

# 설명
1. 정수 배열인 dominoes 내 동일한 숫자들로 이루어진 도미노 쌍의 수를 구하는 문제이다.
- dominoes[i] = [a, b] 이고 dominoes[j] = [c, d]일 때, $a == c && b == d$를 만족하거나 $a == d && b == c$를 만족하는 쌍을 의미한다.

2. 주어진 문제 풀이에 필요한 변수를 정의한다.
- count는 도미노의 두 값을 합쳐서 갯수를 계산할 변수로, 두 값을 연결할 때 값의 상한인 99가 포함되도록 100 크기의 정수 배열로 초기화한다.
- result는 도미노 쌍의 수를 계산할 변수이다.

3. dominoes의 각 도미노들을 domino에 순차적으로 넣어 아래를 수행한다.
- domino[0]의 값이 domino[1]의 값보다 큰 경우, count 내 domino[0]이 십의 자리 domino[1]이 일의 자리에 위치한 값을 증가시키고 해당 값을 result에 더해준다.
- 위의 경우가 아니라면 순서를 바꾸어 count 내 domino[1]이 십의 자리 domino[0]이 일의 자리에 위치한 값을 증가시키고 해당 값을 result에 더해준다.

4. 계산이 완료되면 쌍의 수가 계산된 result를 주어진 문제의 결과로 반환한다.

# 해설
- count는 쌍의 수를 증가시키며 result에 더하면 역순 [Fatorial](https://en.wikipedia.org/wiki/Factorial){:target="_blank"} 계산이 수행되는 것과 같다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfEquivalentDominoPairs.java){:target="_blank"}에서 확인 가능합니다.