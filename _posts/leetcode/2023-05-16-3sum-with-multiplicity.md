---
title: "Leetcode Java 3Sum With Multiplicity"
excerpt: "Leetcode 3Sum With Multiplicity Java"
last_modified_at: 2023-05-16T19:30:00
header:
  image: /assets/images/leetcode/3sum-with-multiplicity.png
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
[Link](https://leetcode.com/problems/3sum-with-multiplicity){:target="_blank"}

# 코드
```java
class Solution {

  public int threeSumMulti(int[] arr, int target) {
    long[] count = new long[101];
    for (int num : arr) {
      count[num]++;
    }
    long result = 0;
    for (int i = 0; i <= 100; i++)
      for (int j = i; j <= 100; j++) {
        int k = target - i - j;
        if (k > 100 || k < 0) {
          continue;
        }
        if (i == j && j == k) {
          result += (count[i] * (count[i] - 1) * (count[i] - 2)) / 6;
        } else if (i == j && j != k) {
          result += ((count[i] * (count[i] - 1)) / 2) * count[k];
        } else if (j < k) {
          result += count[i] * count[j] * count[k];
        }
      }
    return (int) (result % 1000000007);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/3sum-with-multiplicity/submissions/951356541/){:target="_blank"}

# 설명
1. 정수 배열인 arr을 이용하여 아래의 규칙을 만족하는 경우의 수를 구하는 문제이다.
- i < j < k일때, $rr[i] + arr[j] + arr[k] = target$를 만족한다.
- 단, 답이 매우 클 수 있으므로 모듈러 $10^9 + 7$을 이용해 계산한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 숫자의 갯수를 계산할 변수로, 숫자의 최댓값인 100을 이용하여 101 크기로 초기화하고 arr의 모든 값의 수를 넣어준다.
- result는 조건을 만족하는 경우의 수를 저장하기 위한 변수로, 0으로 초기화한다.

3. 0부터 100 이하까지 i를, i부터 100 이하까지 j를 증가시키며 아래를 반복한다.
- k에 $target - i - j$를 넣어준다.
- k가 100보다 크거나 0보다 작은 경우, 숫자 범위에서 벗어나므로 다음 반복을 수행한다.
- i와 j가 같고 j와 k가 같은 경우 세 값이 동일하므로, result에 동일한 세 값을 이용한 경우의 수인 $\frac{count[i] \times (count[i] - 1) \times (count[i] - 2)}{6}$의 값을 더해준다.
- 위의 경우가 아니면서 i와 j의 값이 같고 k만 값이 다른 경우, result에 동일한 두 값과 다른 한 값을 이용한 경우의 수인 $\frac{count[i] * (count[i] - 1)}{2} \times count[k]$의 값을 더해준다.
- 마지막으로 모든 값이 다르면서 j가 k보다 작은 경우, 다른 세 값을 이용한 경우의 수인 $count[i] \times count[j] \times count[k]$의 값을 더해준다.

4. 반복이 완료되면 result에 모듈러 $10^9 + 7$을 적용한 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ThreeSumWithMultiplicity.java){:target="_blank"}에서 확인 가능합니다.