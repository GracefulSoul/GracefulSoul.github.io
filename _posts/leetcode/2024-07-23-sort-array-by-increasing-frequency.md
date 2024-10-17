---
title: "Leetcode Java Sort Array by Increasing Frequency"
excerpt: "Leetcode Easy - 'Sort Array by Increasing Frequency' 문제 Java 풀이"
last_modified_at: 2024-07-23T18:40:00
header:
  image: /assets/images/leetcode/sort-array-by-increasing-frequency.png
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
[Link](https://leetcode.com/problems/sort-array-by-increasing-frequency/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] frequencySort(int[] nums) {
    int[] counts = new int[201];
    for (int num : nums) {
      counts[num + 100]++;
    }
    for (int i = nums.length - 1; i >= 0;) {
      int max = 0;
      int index = -1;
      for (int j = 0; j < 201; j++) {
        if (counts[j] > max) {
          max = counts[j];
          index = j;
        }
      }
      int num = index - 100;
      while (max-- > 0) {
        nums[i--] = num;
      }
      counts[index] = 0;
    }
    return nums;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sort-array-by-increasing-frequency/submissions/1330500566/){:target="_blank"}

# 설명
1. [-100, 100] 범위의 값들 들어있는 nums 내 값의 갯수 별로 오름차순, 동일 갯수 내에서는 내림차순 순으로 값들을 정렬하여 반환하는 문제이다.

2. counts는 nums 내 숫자들의 갯수를 계산할 변수로, 값의 갯수인 201 크기의 정수 배열로 초기화하여 nums내 각 값들에 100을 더한 위치에 해당 숫자의 갯수를 넣어준다.

3. nums의 길이보다 1 작은 위치부터 0 이상일 때 까지 아래를 반복한다.
- max와 index는 갯수의 최댓값과 위치를 저장할 변수로, counts의 모든 값들을 탐색하여 최댓갑과 해당 위치를 넣어준다.
- nums의 i번째 위치에 i를 감소시키며 max번 $index - 100$인 변환 전의 값을 넣어준 후, counts[index]의 값을 0으로 바꿔준다.

4. 반복이 완료되면 정렬된 nums를 주어진 문제의 결과로 반환한다.

# 해설
- nums 내 값의 갯수가 큰 순으로 nums를 채우기 위해서, i는 nums의 거꾸로 시작한다.
- 동일한 값의 갯수가 발생하면 작은 순으로 nums를 채우기 위해서, j는 0부터 탐색하며 가장 많이 발생한 위치를 먼저 max와 index에 넣어준다.
- 위에서 발생한 순서대로 nums를 max번 반복해서 채워주고 counts[index]에 0을 넣음으로써, 해당 값은 다음 탐색에서 무시하게 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SortArrayByIncreasingFrequency.java){:target="_blank"}에서 확인 가능합니다.