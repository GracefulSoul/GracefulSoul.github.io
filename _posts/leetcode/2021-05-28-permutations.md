---
title: "Leetcode Java Permutations"
excerpt: "Leetcode Permutations Java 풀이"
last_modified_at: 2021-05-28T20:50:00
header:
  image: /assets/images/leetcode/permutations.png
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
[Link](https://leetcode.com/problems/permutations/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    this.getPermutations(result, new ArrayList<>(), nums);
    return result;
  }

  private void getPermutations(List<List<Integer>> result, List<Integer> list, int[] nums) {
    if (list.size() == nums.length) {
      result.add(new ArrayList<Integer>(list));
    } else {
      for (int idx = 0; idx < nums.length; idx++) {
        if (list.contains(nums[idx])) {
          continue;
        }
        list.add(nums[idx]);
        this.getPermutations(result, list, nums);
        list.remove(list.size() - 1);
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/499405241/){:target="_blank"}

# 설명
1. 주어진 배열 nums를 이용하여 각 숫자열의 고유 조합을 만드는 문제이다.

2. 재귀 호출을 통해서 주어진 변수 nums로 임시 변수 list에 각 숫자의 고유 조합을 만들어 결과를 담는 변수 result에 주입하여 주어진 문제의 결과를 만들어준다.

3. 임시 변수 list의 길이와 nums의 길이가 같다면, list가 각 숫자열의 고유 조합이므로 결과를 담는 변수 result에 주입한다.

4. 그 외의 경우 주어진 변수 nums로 반복하여 고유 조합을 완성한다.
- nums[idx]의 값이 임시 변수 list에 포함되는 경우는 제외하고 반복을 지속한다.
- nums[idx]의 값이 임시 변수 list에 포함되지 않는 경우, 해당 값을 list에 넣어주고 재귀 호출을 반복한다.
- 재귀 호출이 끝난 경우, list의 마지막 값을 빼고 반복문을 지속한다.

5. 재귀 호출이 모두 완료되면 각 숫자열의 고유 조합을 저장한 result 변수를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/Permutations.java){:target="_blank"}에서 확인 가능합니다.