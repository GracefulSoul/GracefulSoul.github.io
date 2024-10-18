---
title: "Leetcode Java Count Number of Maximum Bitwise-OR Subsets"
excerpt: "Leetcode - 'Count Number of Maximum Bitwise-OR Subsets' 문제 Java 풀이"
last_modified_at: 2024-10-18T19:00:00
header:
  image: /assets/images/leetcode/count-number-of-maximum-bitwise-or-subsets.png
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
[Link](https://leetcode.com/problems/count-number-of-maximum-bitwise-or-subsets/){:target="_blank"}

# 코드
```java
class Solution {

  public int countMaxOrSubsets(int[] nums) {
    int max = 0;
    for (int num : nums) {
      max |= num;
    }
    return this.dfs(nums, 0, 0, max);
  }

  private int dfs(int[] nums, int i, int num, int max) {
    if (i == nums.length) {
      return num == max ? 1 : 0;
    } else {
      return this.dfs(nums, i + 1, num | nums[i], max) + this.dfs(nums, i + 1, num, max);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-number-of-maximum-bitwise-or-subsets/submissions/1426306968/){:target="_blank"}

# 설명
1. nums의 부분 집합의 OR('|') 비트 연산을 수행한 결과가 최대인 부분 집합의 갯수를 구하는 문제이다.

2. max는 OR 비트 연산의 값이 최대인 값을 구하기 위한 변수로, nums의 모든 값을 반복하여 OR의 최댓값을 넣어준다.

3. 4번에서 정의한 dfs(int[] nums, int i, int num, int max)를 i에 0, num에 0을 채워 수행한 결과를 주어진 문제의 결과로 반환한다.

4. DFS 방식으로 갯수를 계산할 dfs(int[] nums, int i, int num, int max) 메서드를 정의한다.
- i가 nums의 길이와 동일한 마지막 위치인 경우, num과 max가 동일하면 1을 아니면 0ㅇ을 반환한다.
- 위의 경우가 아니라면 아래의 두 결과를 더한 값을 반환한다.
  - i의 위치에 $i + 1$을 넣고 num의 위치에 num과 nums[i]를 재귀 호출한 결과인 현재 값을 포함한 부분 배열의 경우에 대한 값.
  - i의 위치에 $i + 1$을 넣어 재귀 호출 한 결과인 현재 값을 제외한 부분 배열의 경우에 대한 값.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountNumberOfMaximumBitwiseORSubsets.java){:target="_blank"}에서 확인 가능합니다.