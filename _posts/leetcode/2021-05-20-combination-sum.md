---
title: "Leetcode Java Combination Sum"
excerpt: "Leetcode - 'Combination Sum' 문제 Java 풀이"
last_modified_at: 2021-05-20T18:10:00
header:
  image: /assets/images/leetcode/combination-sum.png
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
[Link](https://leetcode.com/problems/combination-sum/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> combinationSum(int[] candidates, int target) {
    List<List<Integer>> result = new ArrayList<>();
    this.getCombination(result, new ArrayList<>(), candidates, target, 0);
    return result;
  }

  private void getCombination(List<List<Integer>> result, List<Integer> list, int[] candidates, int target, int start) {
    if (target == 0) {
      result.add(new ArrayList<>(list));
    } else if (target > 0) {
      for (int idx = start; idx < candidates.length; idx++) {
        list.add(candidates[idx]);
        this.getCombination(result, list, candidates, target - candidates[idx], idx);
        list.remove(list.size() - 1);
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/495720930/){:target="_blank"}

# 설명
1. 주어진 배열 candidates의 값들을 이용하여 target의 값이 되는 조합을 탐색하는 문제이다.

2. 탐색한 숫자의 조합을 저장할 컬렉션인 result를 정의한다.

3. 재귀호출을 이용하여 숫자의 조합을 변수 result에 저장한다.
- target이 0이면 숫자 조합의 합이 0이 되는 경우이므로, 해당 값의 조합을 변수 result에 넣는다.
- target이 0보다 작으면 숫자 조합의 합이 target보다 큰 경우이므로, 무시한다.
- target이 0보다 크면 숫자 조합의 합이 target보다 작은 경우이므로, 지속적으로 나머지 숫자의 합이 되는 값을 탐색하기 위해 주어진 배열 candidates를 반복하여 탐색한다.
  - 값을 list에 추가하고, 재귀호출을 통해서 조합을 지속 탐색한다.
  - 주어진 문제의 합이 target보다 커서 무시한 조합이거나, target과 동일하여 result에 저장된 조합인 경우 재귀호출이 종료된다.
  - 마지막으로 저장한 list의 값을 제거하고 다시 반복문을 통해서 조합을 탐색한다.

4. 재귀호출이 종료되면 숫자의 조합을 저장한 result 변수를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CombinationSum.java){:target="_blank"}에서 확인 가능합니다.