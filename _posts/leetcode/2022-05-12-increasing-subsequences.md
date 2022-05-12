---
title: "Leetcode Java Increasing Subsequences"
excerpt: "Leetcode Increasing Subsequences Java 풀이"
last_modified_at: 2022-05-12T22:00:00
header:
  image: /assets/images/leetcode/increasing-subsequences.png
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
[Link](https://leetcode.com/problems/increasing-subsequences/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> findSubsequences(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    this.dfs(nums, result, new ArrayList<>(), 0, Integer.MIN_VALUE);
    return result;
  }

  private void dfs(int[] nums, List<List<Integer>> result, List<Integer> temp, int index, int value) {
    if (index == nums.length) {
      if (temp.size() >= 2) {
        result.add(new ArrayList<Integer>(temp));
      }
      return;
    }
    if (nums[index] >= value) {
      temp.add(nums[index]);
      this.dfs(nums, result, temp, index + 1, nums[index]);
      temp.remove(temp.size() - 1);
    }
    if (nums[index] != value) {
      this.dfs(nums, result, temp, index + 1, value);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/698064808/){:target="_blank"}

# 설명
1. nums 내 최소 두 숫자 이상을 활용하여 모든 부분 배열을 구하는 문제이다.

2. 모든 부분 배열을 넣을 result를 ArrayList로 초기화 한다.

3. 4번에서 정의한 dfs(int[] nums, List<List<Integer>> result, List<Integer> temp, int index, int value) 메서드를 temp에 새 ArrayList, index에 0, value에 int의 가장 작은 숫자를 이용하여 수행한다.

4. DFS 방식으로 결과를 탐색할 dfs(int[] nums, List<List<Integer>> result, List<Integer> temp, int index, int value) 메서드를 정의한다.
- index가 nums의 길이와 동일한 경우, temp의 길이가 2 이상이면 result에 temp를 새 ArrayList 객체로 넣어주고 수행을 중단한다.
- nums의 index번째 값이 value보다 큰 경우 아래를 수행하여 부분 배열을 찾아준다.
  - temp에 해당 값을 넣어주고 index를 증가시키고 nums의 index번째 값을 value에 넣어 재귀 호출을 수행한다.
  - 재귀 호출이 완료되면 temp에 위에서 넣은 값인 마지막 값을 제거해준다.
- nums의 index번째 값이 value와 같지 않은 경우, index를 증가시키고 value로 재귀 호출을 다시 수행하여 또 다른 부분 배열을 완성해준다.

5. 모든 부분 배열을 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/IncreasingSubsequences.java){:target="_blank"}에서 확인 가능합니다.