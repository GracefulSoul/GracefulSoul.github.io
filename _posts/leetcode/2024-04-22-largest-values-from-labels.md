---
title: "Leetcode Java Largest Values From Labels"
excerpt: "Leetcode Largest Values From Labels Java"
last_modified_at: 2024-04-22T18:40:00
header:
  image: /assets/images/leetcode/largest-values-from-labels.png
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
[Link](https://leetcode.com/problems/largest-values-from-labels/){:target="_blank"}

# 코드
```java
class Solution {

  public int largestValsFromLabels(int[] values, int[] labels, int numWanted, int useLimit) {
    int length = values.length;
    int[][] nums = new int[length][2];
    for (int i = 0; i < length; i++) {
      nums[i][0] = values[i];
      nums[i][1] = labels[i];
    }
    Arrays.sort(nums, (a, b) -> b[0] - a[0]);
    int result = 0;
    int[] count = new int[20001];
    for (int[] num : nums) {
      if (count[num[1]] < useLimit) {
        count[num[1]]++;
        numWanted--;
        result += num[0];
      }
      if (numWanted == 0) {
        break;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/largest-values-from-labels/submissions/1238912472/){:target="_blank"}

# 설명
1. 아래의 조건을 만족하는 부분 집합의 최대 점수를 반환하는 문제이다.
- labels의 i번째 요소의 values[i]이다.
- 부분 집합의 크기가 numWanted보다 작거나 같다.
- n개의 요소로 구성된 부분 집합인 s는 useLimit개만큼 동일한 숫자가 포함될 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 values의 길이를 저장한 변수이다.
- nums는 labels와 values를 엮기 위한 배열로, $length \times 2$ 크기의 2차원 정수 배열로 초기화하여 nums[i]에 [values[i], labels[i]]를 넣어준 후 값 기준으로 내림차순 정렬한다..
- result는 결과를 저장할 변수로 0으로 초기화한다.
- count는 값의 갯수를 저장할 변수로, 값의 최대 상한선인 $10^4$보다 1 큰 크기의 정수 배열로 초기화한다.

3. nums의 값을 순차적으로 num에 넣어 아래를 수행한다.
- count[num[1]]의 값이 useLimit보다 작은 경우, 아래를 수행한다.
  - count[num[1]]를 증가시켜 사용한 갯수를 증가시키고, numWanted 값을 감소시켜 갯수를 차감한다.
  - result에 num[0]인 값을 더해준다.
- numWanted가 0인 최대 가능한 부분 집합의 갯수를 채운 경우, 반복을 종료한다.

4. 위의 반복을 통해 최대 점수가 계산된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LargestValuesFromLabels.java){:target="_blank"}에서 확인 가능합니다.