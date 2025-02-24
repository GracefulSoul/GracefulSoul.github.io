---
title: "Leetcode Java Circular Permutation in Binary Representation"
excerpt: "Leetcode - 'Circular Permutation in Binary Representation' 문제 Java 풀이"
last_modified_at: 2025-02-24T15:20:00
header:
  image: /assets/images/leetcode/circular-permutation-in-binary-representation.png
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
[Link](https://leetcode.com/problems/circular-permutation-in-binary-representation/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> circularPermutation(int n, int start) {
    List<Integer> result = new ArrayList<>();
    for (int i = 0; i < 1 << n; i++) {
      result.add(start ^ i ^ i >> 1);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/circular-permutation-in-binary-representation/submissions/1553509643/){:target="_blank"}

# 설명
1. start부터 시작해서 다음부터 1 비트씩 다른 n 길이의 비트 길이의 숫자들을 반환하는 문제이다.

2. result는 결과를 넣을 변수로, ArrayList로 초기화한다.

3. 0부터 1을 n만큼 비트를 이동시킨 값 미만까지 i를 증가시키며 아래를 반복한다.
- result에 start와 i 두 개를 XOR(^) 비트 연산을 수행한 값을 좌측으로 한 번 비트를 이동시킨 값을 넣어준다.

4. 반복을 통해 숫자들을 저장한 result를 주어진 문제의 결과로 반환한다.

# 참고
- 자세한 설명은 [Gray Code](https://en.wikipedia.org/wiki/Gray_code){:target="_blank"}를 읽어본다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CircularPermutationInBinaryRepresentation.java){:target="_blank"}에서 확인 가능합니다.