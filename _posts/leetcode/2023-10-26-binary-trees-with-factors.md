---
title: "Leetcode Java Binary Trees With Factors"
excerpt: "Leetcode Binary Trees With Factors Java"
last_modified_at: 2023-10-26T20:30:00
header:
  image: /assets/images/leetcode/binary-trees-with-factors.png
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
[Link](https://leetcode.com/problems/binary-trees-with-factors){:target="_blank"}

# 코드
```java
class Solution {

  public int numFactoredBinaryTrees(int[] arr) {
    int length = arr.length;
    long[] count = new long[length];
    Arrays.fill(count, 1);
    Arrays.sort(arr);
    long result = 0;
    for (int i = 1; i < length; i++) {
      for (int left = 0, right = i - 1; left <= right;) {
        long product = 1L * arr[left] * arr[right];
        if (product == arr[i]) {
          count[i] += count[left] * count[right];
          if (arr[left] != arr[right]) {
            count[i] += count[left] * count[right];
          }
          left++;
          right--;
        } else if (product < arr[i]) {
          left++;
        } else {
          right--;
        }
      }
    }
    for (long num : count) {
      result += num;
    }
    return (int) (result % 1000000007);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/binary-trees-with-factors/submissions/1084554595/){:target="_blank"}

# 설명
1. arr의 값들을 이용하여 아래의 조건을 만족하게 만들 수 있는 이진 트리의 수를 구하는 문제이다.
- 자식 노드가 존재하는 경우, 자식 노드의 값들을 곱한 값이 부모 노드의 값이 되어야 한다.
- 값이 매우 클 수 있으므로, 모듈러 $10^9 + 7$을 적용한 값으로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 arr의 길이를 저장한 변수이다.
- count는 각 길이 별 만들 수 있는 이진 노드의 갯수를 저장할 배열로, length 크기에 각 갯수가 클 수 있으므로 long형의 정수 배열로 정의하고 모든 위치에 1을 넣어 초기화한다.
- result는 이진 트리의 총 갯수를 저장할 변수로, 각 값의 합이 매우 클 수 있으므로 long형의 0으로 초기화한다.

3. arr의 값들을 오름차순으로 정렬하고 최소 크기인 1부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- left에 0, right에 $i - 1$을 넣고 left가 right 이하일 때 까지 아래를 다시 반복한다.
  - product에 arr[left]의 값과 arr[right]의 값을 long형으로 변환 후 곱하여 넣어준다.
  - product가 arr[i]의 값과 동일한 자식 노드가 가능한 값인 경우, count[i]에 count[left]의 값과 count[right]의 값을 곱한 값을 더한 후 arr[left]의 값과 arr[right]의 값이 다르면 위치를 변경 가능하므로 다시 한 번 더해준다. 그 이후 left를 증가시키고 right를 감소시켜 범위를 좁혀준다.
  - product가 arr[i]의 값보다 작은 경우, left를 증가시켜 하한 범위를 높혀준다.
  - 그 외인 product가 arr[i]의 값보다 큰 경우, right를 감소시켜 상한 범위를 낮춰준다.

4. 반복이 완료되면 count의 모든 값을 result에 넣은 후 모듈러 $10^9 + 7$을 적용한 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryTreesWithFactors.java){:target="_blank"}에서 확인 가능합니다.