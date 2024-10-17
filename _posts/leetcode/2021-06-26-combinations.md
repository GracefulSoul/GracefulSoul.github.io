---
title: "Leetcode Java Combinations"
excerpt: "Leetcode - 'Combinations' 문제 Java 풀이"
last_modified_at: 2021-06-26T07:50:00
header:
  image: /assets/images/leetcode/combinations.png
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
[Link](https://leetcode.com/problems/combinations/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> combine(int n, int k) {
    List<List<Integer>> result = new ArrayList<>();
    if (k == 0) {
      result.add(new ArrayList<Integer>());
      return result;
    } else if (k > n) {
      return result;
    } else {
      result = this.combine(n - 1, k - 1);
      for (List<Integer> list : result) {
        list.add(n);
      }
      result.addAll(this.combine(n - 1, k));
      return result;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/513189707/){:target="_blank"}

# 설명
1. 1부터 주어진 정수 n까지의 숫자들을 이용하여 주어진 정수 k 크기의 배열을 중복되지 않은 숫자들의 조합을 만들어 배열로 반환하는 문제이다.

2. 중복되지 않은 숫자들의 조합을 넣을 배열 result를 정의한다.

3. 재귀 호출을 통해서 주어진 문제를 해결한다.
- k가 0인 경우, result에 조합을 만들기 위한 새 배열을 만들어 반환한다.
- k가 n보다 큰 경우, 주어진 배열의 크기 n보다 주어진 숫자 k가 적기 때문에 result를 그대로 반환한다.
- 그 외의 경우, 배열을 만들기 위해 result를 $n - 1$과 $k - 1$로 재귀 호출을 수행한 결과를 받아서 result 내 배열에 n을 모두 넣어주고, result에 $n - 1$과 k로 재귀 호출을 수행한 결과를 합쳐서 반환한다.

4. 마지막으로 3번의 마지막 경우를 통해 최종 결과가 생성되고, 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/Combinations.java){:target="_blank"}에서 확인 가능합니다.