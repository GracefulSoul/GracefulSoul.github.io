---
title: "Leetcode Java Two Sum II - Input array is sorted"
excerpt: "Leetcode Two Sum II - Input array is sorted Java 풀이"
last_modified_at: 2021-09-18T16:00:00
header:
  image: /assets/images/leetcode/two-sum-ii-input-array-is-sorted.png
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
[Link](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] twoSum(int[] numbers, int target) {
    int left = 0;
    int right = numbers.length - 1;
    while (left < right) {
      if (numbers[left] + numbers[right] == target) {
        break;
      } else if (numbers[left] + numbers[right] > target) {
        right--;
      } else {
        left++;
      }
    }
    return new int[] { left + 1, right + 1 };
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/556821729/){:target="_blank"}

# 설명
1. 주어진 배열 numbers은 오름차순으로 정렬된 정수 배열로, 두 값을 이용하여 target을 만족시키는 값의 순번을 반환하는 문제이다.
- 배열 내 index가 아니라 배열 내 몇 번째에 위치한 값인지를 반환하는것이다.

2. 문제 풀이를 위한 변수를 정의한다.
- left는 좌측에서 left-right 순으로 값을 탐색하여 두 값중 작은 값의 index를 저장하는 변수이다.
- right는 우측에서 right-left 순으로 값을 탐색하여 두 값중 큰 값의 index를 저장하는 변수이다.

3. left가 right보다 작을 때 까지 두 값의 합이 target을 만족시키는 값의 index를 탐색한다.
- $numbres[left] + numbers[right]$의 값이 target 값과 동일하면, 반복을 종료한다.
- $numbres[left] + numbers[right]$의 값이 target 값보다 크면, right를 감소시켜 더 작은 값을 이용하여 비교를 한다.
- $numbres[left] + numbers[right]$의 값이 target 값보다 작으면, left를 증가시켜 더 큰 값을 이용하여 비교를 한다.

4. 반복이 완료되면 left와 right를 각각 1씩 증가시키고 배열로 만들어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TwoSumII_InputArrayIsSorted.java){:target="_blank"}에서 확인 가능합니다.