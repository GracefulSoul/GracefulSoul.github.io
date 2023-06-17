---
title: "Leetcode Java Make Array Strictly Increasing"
excerpt: "Leetcode Make Array Strictly Increasing Java"
last_modified_at: 2023-06-17T14:00:00
header:
  image: /assets/images/leetcode/make-array-strictly-increasing.png
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
[Link](https://leetcode.com/problems/make-array-strictly-increasing){:target="_blank"}

# 코드
```java
class Solution {

  public int makeArrayIncreasing(int[] arr1, int[] arr2) {
    Arrays.sort(arr2);
    Map<Integer, Integer> dp = new HashMap<>();
    dp.put(-1, 0);
    for (int num : arr1) {
      Map<Integer, Integer> temp = new HashMap<>();
      for (Map.Entry<Integer, Integer> entry : dp.entrySet()) {
        if (num > entry.getKey()) {
          temp.put(num, Math.min(temp.getOrDefault(num, Integer.MAX_VALUE), entry.getValue()));
        }
        int index = Arrays.binarySearch(arr2, entry.getKey() + 1);
        if (index < 0) {
          index = -index - 1;
        }
        if (index < arr2.length) {
          temp.put(arr2[index], Math.min(entry.getValue() + 1, temp.getOrDefault(arr2[index], Integer.MAX_VALUE)));
        }
      }
      dp = temp;
    }
    return dp.isEmpty() ? -1 : Collections.min(dp.values());
  }

}
```

# 결과
[Link](https://leetcode.com/problems/make-array-strictly-increasing/submissions/973114588/){:target="_blank"}

# 설명
1. arr1의 값들을 arr2의 값으로 대체하여 순차적으로 증가시키는 배열로 변환하는 문제이다.
- 순차적으로 증가하는 배열로 변환하지 못하는 경우, -1을 반환한다.

2. arr2의 값을 오름차순으로 정렬한다.

3. dp는 값을 바꾼 값을 저장할 변수로, HashMap으로 초기화하여 key와 value가 -1과 0인 초기 값을 넣어준다.

4. arr1의 모든 값을 num에 순차적으로 넣고 아래를 수행한다.
- temp는 dp를 이용하여 대체할 값을 저장할 변수로, HashMap으로 초기화한다.
- dp의 값들을 순차적으로 entry에 넣고 아래를 수행한다.
  - num이 entry의 key 값보다 큰 경우, temp의 num번째 값을 꺼내되 값이 없으면 정수의 최대값을 가져와 그 값과 entry의 value 값 중 작은 값을 넣어준다.
  - index에 arr2에서 entry의 key 값보다 1 큰 숫자의 다음 위치를 찾아 넣어준다.
  - 만일 index가 0보다 작은 경우, index를 양수로 변환하여 1을 빼준다.
  - index가 arr2의 길이보다 작은 경우, temp의 arr2[index] 값의 위치에 entry의 value 값보다 1 큰 값과 temp의 arr2[index]번째 값을 꺼내되 값이 없으면 정수의 최댓 값을 가져와 두 값 중 작은 값을 넣어준다.
- dp에 변환된 값이 저장된 temp를 넣어준다.

5. dp가 비어으면 변환이 되지 않으므로 -1을, 비어있지 않으면 dp 내 value 중 가장 작은 값을 꺼내서 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MakeArrayStrictlyIncreasing.java){:target="_blank"}에서 확인 가능합니다.