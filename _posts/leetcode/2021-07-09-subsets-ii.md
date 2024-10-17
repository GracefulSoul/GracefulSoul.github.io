---
title: "Leetcode Java Subsets II"
excerpt: "Leetcode - 'Subsets II' 문제 Java 풀이"
last_modified_at: 2021-07-09T18:00:00
header:
  image: /assets/images/leetcode/subsets-ii.png
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
[Link](https://leetcode.com/problems/subsets-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> subsetsWithDup(int[] nums) {
    Arrays.sort(nums);
    List<List<Integer>> result = new ArrayList<>();
    this.recursive(result, new ArrayList<>(), nums, 0);
    return result;
  }

  private void recursive(List<List<Integer>> result, List<Integer> temp, int[] nums, int start) {
    result.add(new ArrayList<>(temp));
    for (int idx = start; idx < nums.length; idx++) {
      if (idx > start && nums[idx] == nums[idx - 1]) {
        continue;
      }
      temp.add(nums[idx]);
      this.recursive(result, temp, nums, idx + 1);
      temp.remove(temp.size() - 1);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/519623450/){:target="_blank"}

# 설명
1. 정렬되지 않은 주어진 배열 nums 안의 값들을 이용하여 중복되지 않은 부분 배열들을 만드는 문제이다.

2. 중복된 부분 배열 생성을 사전에 방지하기 위해서 nums를 오름차순으로 정렬한다.

3. 부분 배열들을 넣을 result 변수를 선언하고, 재귀 호출을 통해 부분 배열을 만들어 넣어준다.
- 부분 배열을 만드는 temp를 새 ArrayList 객체로 생성하여 result에 넣어준다.
- 전달받은 start부터 nums의 길이 미만까지 반복을 통해 부분 배열을 생성한다.
- idx가 start보다 크고 nums[idx]와 nums[idx - 1]의 값이 동일한 경우, 중복된 값이므로 무시하고 반복을 계속 한다.
- 위의 경우가 아닌 경우 temp에 nums[idx]를 넣고 start에 idx + 1 값을 넣어 재귀 호출을 수행한다.
- 재귀 호출이 끝나면 temp의 마지막 값을 제거하고 반복을 계속 한다.

4. 재귀 호출이 완료되면 중복되지 않은 부분 배열들을 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SubsetsII.java){:target="_blank"}에서 확인 가능합니다.