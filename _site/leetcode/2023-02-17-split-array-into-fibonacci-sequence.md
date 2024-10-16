---
title: "Leetcode Java Split Array into Fibonacci Sequence"
excerpt: "Leetcode Split Array into Fibonacci Sequence Java"
last_modified_at: 2023-02-17T19:30:00
header:
  image: /assets/images/leetcode/split-array-into-fibonacci-sequence.png
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
[Link](https://leetcode.com/problems/split-array-into-fibonacci-sequence){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> splitIntoFibonacci(String num) {
    List<Integer> result = new ArrayList<>();
    if (this.dfs(num, result, 0)) {
      return result;
    }
    return new ArrayList<>();
  }

  private boolean dfs(String num, List<Integer> result, int index) {
    if (index == num.length()) {
      return result.size() > 2;
    }
    int n = 0;
    for (int i = index; i < num.length(); i++) {
      n = (n * 10) + num.charAt(i) - '0';
      if (n < 0) {
        return false;
      }
      if (result.size() < 2 || result.get(result.size() - 2) + result.get(result.size() - 1) == n) {
        result.add(n);
        if (this.dfs(num, result, i + 1)) {
          return true;
        }
        result.remove(result.size() - 1);
      }
      if (num.charAt(index) == '0') {
        break;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/split-array-into-fibonacci-sequence/submissions/899697460/){:target="_blank"}

# 설명
1. num을 이용하여 그룹으로 구성된 값들 간 아래의 구성과 같은 피보나치 수열과 같은 조건을 만족하는 그룹이 되도록 만드는 문제이다.
- num이 "123456579"이면, $1 + 4 = 5$, $2 + 5 = 7$ $3 + 6 = 9$인 [123, 456, 579]으로 구성이 가능하다.
- 피보나치 수열과 동일하게 위의 구성을 만족하기 위해서는 그룹은 3개 이상으로 구성된다.

2. 결과를 넣을 result를 ArrayList로 초기화한다.

3. 4번에서 정의한 dfs(String num, List<Integer> result, int index) 메서드를 수행한 결과가 true면 구성이 완료되었으므로 result를 주어진 문제의 결과로 반환한다.

4. DFS 방식으로 그룹을 만들 dfs(String num, List<Integer> result, int index) 메서드를 정의한다.
- index가 num의 길이와 동일하면 result의 길이가 2 이상인지 검증한 결과를 반환한다.
- n은 숫자를 계산할 변수로, 0으로 초기화하고 index부터 num의 길이 미만까지 i를 증가시키며 아래를 수행한다.
  - n에 기존 값의 자릿수를 증가시키고, num의 i번째 문자를 숫자로 변환한 값을 더해준다.
  - n이 0 미만인 경우, 만족하는 결과를 만들 수 없으므로 false를 반환한다.
  - result의 크기가 2개 미만이거나, result의 마지막 두 값의 합이 n인 경우 피보나치 수열과 같은 조건을 만족하므로 result에 n을 넣고, index에 $i + 1$을 넣어 재귀 호출을 수행한 결과가 true면 true를 반환하고 마지막 값을 제거한다.
  - num의 index번쨰 값이 0인 경우, 반복을 중지시킨다.
- 반복이 정상적으로 완료되면 조건을 만족하지 않으므로 false를 반환한다.

5. 3번의 재귀 호출이 정상적으로 종료되면 만족한 그룹을 생성하지 못하므로, 새 ArrayList를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SplitArrayIntoFibonacciSequence.java){:target="_blank"}에서 확인 가능합니다.