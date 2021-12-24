---
title: "Leetcode Java Count of Smaller Numbers After Self"
excerpt: "Leetcode Count of Smaller Numbers After Self Java 풀이"
last_modified_at: 2021-12-24T12:00:00
header:
  image: /assets/images/leetcode/count-of-smaller-numbers-after-self.png
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
[Link](https://leetcode.com/problems/count-of-smaller-numbers-after-self/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> countSmaller(int[] nums) {
    int length = nums.length;
    Integer[] result = new Integer[length];
    int min = Integer.MAX_VALUE;
    int max = Integer.MIN_VALUE;
    for (int num : nums) {
      min = Math.min(min, num);
    }
    for (int idx = 0; idx < length; idx++) {
      nums[idx] = nums[idx] - min + 1;
      max = Math.max(max, nums[idx]);
    }
    int[] tree = new int[max + 1];
    for (int idx = length - 1; idx >= 0; idx--) {
      result[idx] = this.get(tree, nums[idx] - 1);
      this.update(tree, nums[idx]);
    }
    return Arrays.asList(result);
  }

  private void update(int[] tree, int index) {
    int length = tree.length;
    while (index < length) {
      tree[index]++;
      index += (index & -index);
    }
  }

  private int get(int[] tree, int index) {
    int count = 0;
    while (index > 0) {
      count += tree[index];
      index -= (index & -index);
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/606262252/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums의 값들을 이용하여 특정 위치의 값은 해당 위치 이후의 값들 중 자신보다 작은 값이 몇 개 존재하는지 각각 세서 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장하기 위한 변수이다.
- result는 nums와 동일한 위치에 존재하는 값의 결과를 저장하기 위한 배열로, length의 크기로 초기화한다.
- min은 nums 내 가장 작은 값을 저장할 배열로, Integer의 가장 큰 값으로 초기화하고 nums를 순회하며 가장 작은 값을 찾아 넣어준다.
- max는 nums 내 가장 큰 값을 저장할 배열로, Integer의 가장 작은 값으로 초기화하고 nums를 순회하며 가장 큰 값을 찾아 넣어준다.
  - 단, 순회하면서 배열의 크기를 최소한으로 사용하기 위해 nums의 idx번째 값에 $nums[idx] - min + 1$ 값을 넣어 값들을 0 기준으로 평준화 시켜주고, 해당 값을 이용하여 큰 값을 산정한다.

3. Binary index tree로 사용할 tree 배열을 $max + 1$ 크기로 정의하고, nums를 역순으로 탐색하여 결과를 세기 위해서 $length - 1$부터 0까지 반복을 수행한다.
- reulst[idx]에 tree와 nums의 $idx - 1$ 값을 이용하여 갯수를 세서 넣어준다.
  - index가 0보다 클 때 까지 반복하여 count에 tree의 index번째 값을 넣어주고, index에 index와 -index 값을 AND(&) 비트 연산하여 더하여 반복을 계속 수행한다.
- tree에 nums의 idx 값을 이용하여 값을 수정해준다.
  - index가 tree의 길이보다 작을 떄 까지 반복하여 tree의 index번째 값을 증가시키고, index에 index와 -index 값을 AND(&) 비트 연산하여 더하여 반복을 계속 수행한다.

4. 3번을 통해 계산된 특정 위치 이후의 값들 중 자신보다 작은 값의 갯수를 산정한 result를 List로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountOfSmallerNumbersAfterSelf.java){:target="_blank"}에서 확인 가능합니다.