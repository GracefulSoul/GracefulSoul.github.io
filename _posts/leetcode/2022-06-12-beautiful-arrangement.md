---
title: "Leetcode Java Beautiful Arrangement"
excerpt: "Leetcode Beautiful Arrangement Java"
last_modified_at: 2022-06-12T10:00:00
header:
  image: /assets/images/leetcode/beautiful-arrangement.png
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
[Link](https://leetcode.com/problems/beautiful-arrangement/){:target="_blank"}

# 코드
```java
class Solution {

  public int countArrangement(int n) {
    int[] array = new int[n];
    for (int idx = 0; idx < n; idx++) {
      array[idx] = idx + 1;
    }
    return this.recursive(array, n - 1);
  }

  private int recursive(int[] array, int index) {
    if (index == 0) {
      return 1;
    }
    int count = 0;
    for (int idx = index; idx >= 0; idx--) {
      this.swap(array, index, idx);
      int num = index + 1;
      if (array[index] % num == 0 || num % array[index] == 0) {
        count += this.recursive(array, index - 1);
      }
      this.swap(array, index, idx);
    }
    return count;
  }

  private void swap(int[] array, int i, int j) {
    int temp = array[i];
    array[i] = array[j];
    array[j] = temp;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/720042447/){:target="_blank"}

# 설명
1. 1 ~ n까지 아래의 조건을 만족하는 배열의 수를 구하는 문제이다.
- i는 1 <= i <= n 를 만족한다.
- perm[i]는 i로 나눌 수 있다.
- i 는 perm[i]으로 나눌 수 있다.

2. n 크기의 배열인 array를 정의하여 모든 자리에 1부터 n까지 값을 넣어준다.

3. 4번에서 정의한 recursive(int[] array, int index) 결과를 주어진 문제의 결과로 반환한다.

4. 재귀 호출을 통해 1번의 조건을 만족하는 경우의 수를 계산하기 위한 recursive(int[] array, int index) 메서드를 정의한다.
- index가 0인 경우, 계산할 필요 없이 1을 반환한다.
- count를 0으로 정의하고 index부터 0까지 idx를 감소시키며 계산을 수행한다.
  - array의 index번째 값과 idx번째 값을 바꾸어준다.
  - num에 $ndex + 1$인 위치를 숫자로 변환한 값을 넣어준다.
  - 1번에서 정의한 조건인 array[index]를 num으로, num을 array[index]로 나눌 수 있는지 검증하여 count에 $index - 1$을 넣어 재귀 호출 한 결과를 더해준다.
  - 다시 array의 index번째 값과 idx번쨰 값을 바꾸어 원상복구한다.
- 반복이 완료되면 count를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ContiguousArray.java){:target="_blank"}에서 확인 가능합니다.