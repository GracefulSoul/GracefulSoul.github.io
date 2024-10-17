---
title: "Leetcode Java Relative Sort Array"
excerpt: "Leetcode Easy - 'Relative Sort Array' 문제 Java 풀이"
last_modified_at: 2024-06-11T19:00:00
header:
  image: /assets/images/leetcode/relative-sort-array.png
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
[Link](https://leetcode.com/problems/relative-sort-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] relativeSortArray(int[] arr1, int[] arr2) {
    int[] count = new int[1001];
    for (int num : arr1) {
      count[num]++;
    }
    int index = 0;
    for (int num : arr2) {
      while (count[num]-- > 0) {
        arr1[index++] = num;
      }
    }
    for (int i = 0; index < arr1.length && i < 1001; i++) {
      while (count[i]-- > 0) {
        arr1[index++] = i;
      }
    }
    return arr1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/relative-sort-array/submissions/1284756861/){:target="_blank"}

# 설명
1. 정수 배열 arr2의 값들의 순서대로 arr1을 정렬하고 arr2 내 없는 값들은 정렬 된 이후 순서로 오름차순 정렬하여 넣어주는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 arr1 내 값들의 갯수를 저장할 변수로, arr1의 모든 값을 반복하여 갯수를 계산해준다.
- index는 arr1의 값들을 정렬된 순서대로 넣어주기위한 위치 변수로, 첫 위치인 0으로 초기화한다.

3. arr2의 값들을 순차적으로 반복하여 count 내 값들의 갯수만큼 순서대로 arr1에 넣어준다.

4. 0부터 1001 미만일 때 까지 i를 증가시키고, index가 arr1의 길이 미만일 때 까지 count[i]의 값을 arr1 내 순차적으로 넣어준다.

5. 조건대로 정렬된 arr1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RelativeSortArray.java){:target="_blank"}에서 확인 가능합니다.