---
title: "Leetcode Java Pancake Sorting"
excerpt: "Leetcode Medium - 'Pancake Sorting' 문제 Java 풀이"
last_modified_at: 2023-08-06T08:40:00
header:
  image: /assets/images/leetcode/pancake-sorting.png
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
[Link](https://leetcode.com/problems/pancake-sorting){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> pancakeSort(int[] arr) {
    List<Integer> result = new ArrayList<>();
    for (int i = arr.length, j; i > 0; i--) {
      for (j = 0; arr[j] != i; j++);
      this.reverse(arr, j + 1);
      result.add(j + 1);
      this.reverse(arr, i);
      result.add(i);
    }
    return result;
  }

  private void reverse(int[] arr, int k) {
    for (int i = 0, j = k - 1; i < j; i++, j--) {
      int temp = arr[i];
      arr[i] = arr[j];
      arr[j] = temp;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/pancake-sorting/submissions/1013346123/){:target="_blank"}

# 설명
1. arr을 팬케이크 플립하여 오름차순 정렬하기 위해 선택한 숫자들을 반환하는 문제이다.
- 팬케이크 플립은 1 <= k <= arr.length을 만족하는 k를 선택하여 [0, $k - 1$] 범위의 값들을 반전시킨다.

2. result는 결과를 저장할 변수로, ArrayList로 초기화한다.

3. arr의 길이부터 0 초과일 때 까지 i를 감소시키고, j를 정의하여 아래를 반복한다.
- 0부터 arr[j]의 값이 i가 아닐 때 까지 j를 증가시켜준다.
- arr의 [0, $j + 1$] 범위의 값을 반전시키고 선택한 $j + 1$을 result에 넣어준다.
- arr의 [0, i] 범위의 값을 반전시키고 선택한 i를 result에 넣어준다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PancakeSorting.java){:target="_blank"}에서 확인 가능합니다.