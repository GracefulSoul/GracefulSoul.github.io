---
title: "Leetcode Java Permutations II"
excerpt: "Leetcode Permutations II Java 풀이"
last_modified_at: 2021-05-29T09:30:00
header:
  image: /assets/images/leetcode/permutations-ii.png
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
[Link](https://leetcode.com/problems/permutations-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> permuteUnique(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    this.swap(nums);
    this.getPermutations(result, new ArrayList<>(), nums, new boolean[nums.length]);
    return result;
  }

  private void getPermutations(List<List<Integer>> result, List<Integer> list, int[] nums, boolean[] used) {
    if (list.size() == nums.length) {
      result.add(new ArrayList<Integer>(list));
    } else {
      for (int idx = 0; idx < nums.length; idx++) {
        if (used[idx] || (idx > 0 && nums[idx - 1] == nums[idx] && !used[idx - 1])) {
          continue;
        }
        list.add(nums[idx]);
        used[idx] = true;
        this.getPermutations(result, list, nums, used);
        used[idx] = false;
        list.remove(list.size() - 1);
      }
    }
  }

  private void swap(int[] nums) {
    for (int i = 0; i < nums.length - 1; i++) {
      for (int j = i + 1; j < nums.length; j++) {
        if (nums[i] > nums[j]) {
          int temp = nums[j];
          nums[j] = nums[i];
          nums[i] = temp;
        }
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/499650179/){:target="_blank"}

# 설명
1. 이전에 Permutations(../permutations)와 비슷한 문제이지만, 주어진 배열 nums에 중복된 숫자열이 들어가는 것과 순서에 영향을 받는 것이 이 문제의 초점이다.

2. 기본 순서를 정렬하기 위해 정렬을 통해 오름차순 정렬을 수행해준다.
- 정렬은 Arrays.sort()로 사용이 가능하지만, [선택 정렬](https://en.wikipedia.org/wiki/Selection_sort){:target="_blank"}로 구현하였다.

3. 재귀 호출을 통해서 주어진 변수 nums로 임시 변수 list에 각 숫자의 고유 조합을 만들어 결과를 담는 변수 result에 주입하여 주어진 문제의 결과를 만들어준다.

4. 임시 변수 list의 길이와 nums의 길이가 같다면, list가 각 숫자열의 고유 조합이므로 결과를 담는 변수 result에 주입한다.

5. 그 외의 경우 주어진 변수 nums로 반복하여 usable을 통해 숫자열의 조합을 완성한다.
- used[idx]의 값이 true이면 이미 사용한 값이므로, 다음 반복을 진행한다.
- idx가 0보다 크고, nums\[$idx - 1$\]의 값이 nums[idx]의 값과 동일하며, $idx - 1$번째 자리의 값이 사용중이지 않다면, 다음 반복을 진행한다.
- 위의 두 경우를 제외하면 list에 nums[idx] 값을 넣고, 해당 위치의 값을 사용 중으로 체크하기 위해 used[idx]의 값을 true로 주입하여 재귀 호출을 반복한다.
- 재귀 호출이 끝난 경우 해당 위치의 값을 제거하므로 used[idx]의 값을 false로 주입하고, list의 마지막 값을 제거하고 반복문을 지속한다.

6. 재귀 호출이 모두 완료되면 각 숫자열의 고유 조합을 저장한 result 변수를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PermutationsII.java){:target="_blank"}에서 확인 가능합니다.