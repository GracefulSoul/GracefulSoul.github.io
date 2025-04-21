---
title: "Leetcode Java Count the Hidden Sequences"
excerpt: "Leetcode - 'Count the Hidden Sequences' 문제 Java 풀이"
last_modified_at: 2025-04-21T21:12:00
header:
  image: /assets/images/leetcode/count-the-hidden-sequences.png
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
[Link](https://leetcode.com/problems/count-the-hidden-sequences/){:target="_blank"}

# 코드
```java
class Solution {

  public int numberOfArrays(int[] differences, int lower, int upper) {
    long sum = 0;
    long max = 0;
    long min = 0;
    for (int difference : differences) {
      sum += difference;
      max = Math.max(max, sum);
      min = Math.min(min, sum);
    }
    return (int) Math.max(0, (upper - lower) - (max - min) + 1);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-the-hidden-sequences/submissions/1613501751/){:target="_blank"}

# 설명
1. 아래의 규칙을 만족하는 정수 배열인 differences를 이용하여 [lower, upper] 범위 내 만족하는 조합의 수를 구하는 문제이다.
- hidden은 숨겨진 조합으로, 인접한 두 값의 차이가 differences 배열이 된다.
- 즉, $differences[i] = hidden[i + 1] - hidden[i]$를 만족한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 differences 내 값들의 합계를 구하기 위한 변수로, 합계가 매우 클 수 있으므로 long 타입의 0으로 초기화한다.
- max와 min은 누계된 값들 중 최댓값과 최솟값을 저장하기 위한 변수로, sum과 동일하게 long 타입의 0으로 초기화한다.

3. differences의 값들을 순차적으로 difference에 넣어 아래를 수행한다.
- sum에 difference의 값을 누계한다.
- max 와 min에 자기 자신과 sum 중 최댓값과 최솟값을 넣어준다.

4. 반복이 완료되면 0과 $(upper - lower) - (max - min) + 1$인 [lower, upper] 범위 내 만족하는 조합의 수를 주어진 문제의 결과로 반환한다.

# 해설
- 누계된 값들을 이용한 max와 min의 차잇값은 범위 내 최대 폭을 나타내므로, [lower, upper] 범위에서는 아래와 같은 계산식이 성립한다.
  - $upper - lower < max - min$의 경우, [lower, upper] 범위 내 hidden 배열은 존재하지 않는다.
  - $upper - lower = max - min$의 경우, [lower, upper] 범위 내 hidden 배열이 한 개만 존재한다.
  - 위의 공식을 반복하여 $upper - lower = max - min + n$의 경우, [lower, upper] 범위 내 hidden 배열이 $n + 1$ 개가 존재한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountTheHiddenSequences.java){:target="_blank"}에서 확인 가능합니다.