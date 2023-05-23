---
title: "Leetcode Java Three Equal Parts"
excerpt: "Leetcode Three Equal Parts Java"
last_modified_at: 2023-05-23T18:55:00
header:
  image: /assets/images/leetcode/three-equal-parts.png
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
[Link](https://leetcode.com/problems/three-equal-parts){:target="_blank"}

# 코드
```java
class Solution {

  public int[] threeEqualParts(int[] arr) {
    int count = 0;
    for (int num : arr) {
      if (num == 1) {
        count++;
      }
    }
    if (count == 0) {
      return new int[] { 0, 2 };
    }
    if (count % 3 != 0) {
      return new int[] { -1, -1 };
    }
    int index = 0;
    for (int i = arr.length - 1, oneThird = count / 3; i >= 0; i--) {
      if (arr[i] == 1 && --oneThird == 0) {
        index = i;
        break;
      }
    }
    int first = this.findIndex(arr, 0, index);
    if (first < 0) {
      return new int[] { -1, -1 };
    }
    int second = this.findIndex(arr, first + 1, index);
    if (second < 0) {
      return new int[] { -1, -1 };
    }
    return new int[] { first, second + 1 };
  }

  private int findIndex(int[] arr, int left, int right) {
    while (arr[left] == 0) {
      left++;
    }
    while (right < arr.length) {
      if (arr[left++] != arr[right++]) {
        return -1;
      }
    }
    return left - 1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/three-equal-parts/submissions/955703185/){:target="_blank"}

# 설명
1. 0과 1로 구성된 arr의 이진 표현법의 값이 동일한 세 부분 배열로 나누기 위한 위치를 찾는 문제이다.
- 단, 나눌 수 없는 경우는 [-1, -1]을 주어진 문제의 결과로 반환한다.
- 부분 배열로 나누는 위치가 [i, j]인 경우 $i + 1$ < j를 만족한다.

2. count는 1의 수를 저장할 변수로, arr 내 1의 갯수를 저장한다.

3. count가 0이면 아무 위치로 분할해도 1의 갯수는 같으므로, 조건에 맞도록 [0, 2]를 주어진 문제의 결과로 반환한다.

4. count가 3의 배수가 아닌 경우 1의 수가 동일한 세 부분 배열로 나눌 수 없으므로, [-1, -1]을 주어진 문제의 결과로 반환한다.

5. index는 1의 수가 $\frac{1}{3}$인 위치를 저장하기 위한 변수로, arr을 역순으로 탐색하여 해당 위치를 index에 저장한다.

6. arr의 부분 배열로 나누기 위한 findIndex(int[] arr, int left, int right) 메서드를 정의한다.
- arr의 left번째 값이 0인 경우 left를 계속 증가시켜 1의 위치로 이동시킨다.
- right가 arr의 길이 미만까지 arr의 left번째 갑솨 right번째 값이 동일한지 검증하여, 동일하지 않으면 -1을 반환한다.
- 반복이 완료되면 나누기 위한 위치 값인 $left - 1$을 반환한다.

7. first에 0부터 index까지 6번의 findIndex(int[] arr, int left, int right) 메서드를 수행한 결과를 넣고, 해당 값이 0보다 작은 위치 값을 탐색하지 못한경우 [-1, -1]을 주어진 문제의 결과로 반환한다.

8. second에 $fisrt + 1$부터 index까지 6번의 findIndex(int[] arr, int left, int right) 메서드를 수행한 결과를 넣고, 해당 값이 0보다 작은 위치 값을 탐색하지 못한경우 [-1, -1]을 주어진 문제의 결과로 반환한다.

9. 위치 탐색이 완료되면 [first, $second + 1$]을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ThreeEqualParts.java){:target="_blank"}에서 확인 가능합니다.