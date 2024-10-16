---
title: "Leetcode Java Check If Array Pairs Are Divisible by k"
excerpt: "Leetcode Check If Array Pairs Are Divisible by k Java"
last_modified_at: 2024-10-01T15:20:00
header:
  image: /assets/images/leetcode/check-if-array-pairs-are-divisible-by-k.png
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
[Link](https://leetcode.com/problems/check-if-array-pairs-are-divisible-by-k/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canArrange(int[] arr, int k) {
    int[] counts = new int[k];
    for (int num : arr) {
      counts[((num % k) + k) % k]++;
    }
    if (counts[0] % 2 != 0) {
      return false;
    }
    for (int i = 1; i <= k / 2; i++) {
      if (counts[i] != counts[k - i]) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/check-if-array-pairs-are-divisible-by-k/submissions/1407885522/){:target="_blank"}

# 설명
1. arr의 값 중 두 숫자씩 쌍을 이룬 값들의 합이 k로 나눌 수 있는 검증하는 문제이다.

2. counts는 arr의 값을 k로 나누기 위한 값을 저장할 변수로, k 크기의 정수 배열로 초기화한 후 arr의 모든 값을 순차적으로 k로 나눈 나머지 값에 k를 더한 후 다시 k로 나눈 나머지 값에 해당하는 값을 증가시켜준다.

3. counts[0]의 값을 2로 나눈 결과가 0이 아닌 k 배수가 홀수인 경우, 각 값들의 합이 k로 나눌 수 없으므로 false를 주어진 문제의 결과로 반환한다.

4. 1부터 $\frac{k}{2}$ 이하까지 i를 증가시키며 counts[i]의 값이 counts[$k -i$]의 값과 다른 두 값을 합친 경우, k의 배수가 되지 않는 경우 false를 주어진 문제의 결과로 반환하다.

5. 모든 검증이 끝나면 조건을 만족하므로 true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CheckIfArrayPairsAreDivisibleByK.java){:target="_blank"}에서 확인 가능합니다.