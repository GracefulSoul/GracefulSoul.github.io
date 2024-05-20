---
title: "Leetcode Java Sum of All Subset XOR Totals"
excerpt: "Leetcode Sum of All Subset XOR Totals Java"
last_modified_at: 2024-05-20T18:00:00
header:
  image: /assets/images/leetcode/sum-of-all-subset-xor-totals.png
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
[Link](https://leetcode.com/problems/sum-of-all-subset-xor-totals/){:target="_blank"}

# 코드
```java
class Solution {

  public int subsetXORSum(int[] nums) {
    return this.dfs(nums, 0, 0);
  }

  private int dfs(int[] nums, int index, int curr) {
    if (index == nums.length) {
      return curr;
    } else {
      return this.dfs(nums, index + 1, curr ^ nums[index]) + this.dfs(nums, index + 1, curr);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sum-of-all-subset-xor-totals/submissions/1262927891/){:target="_blank"}

# 설명
1. nums내 값들을 이용한 부분 배열들의 값들을 XOR 비트 연산한 값을 더한 결과를 반환하는 문제이다.

2. 3번에서 정의한 dfs(int[] nums, int index, int curr) 메서드의 index와 curr에 0을 넣고 수행한 결과를 주어진 문제의 결과로 반환한다.

3. DFS 방식으로 합계하기 위한 dfs(int[] nums, int index, int curr) 메서드를 정의한다.
- index와 length가 동일한 마지막 위치의 값인 경우, curr을 반환한다.
- 위의 경우가 아니라면 아래의 두 값의 합을 반환한다.
  - index에 $index + 1$과 curr에 curr과 nums[index]의 XOR 비트 연산을 수행한 값을 넣어 재귀 호출을 수행한 결과.
  - index에 $index + 1$을 넣어 재귀 호출을 수행한 결과.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SumOfAllSubsetXORTotals.java){:target="_blank"}에서 확인 가능합니다.