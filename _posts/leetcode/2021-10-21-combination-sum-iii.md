---
title: "Leetcode Java Combination Sum III"
excerpt: "Leetcode Combination Sum III Java 풀이"
last_modified_at: 2021-10-21T12:00:00
header:
  image: /assets/images/leetcode/combination-sum-iii.png
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
[Link](https://leetcode.com/problems/combination-sum-iii/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> combinationSum3(int k, int n) {
    List<List<Integer>> result = new ArrayList<>();
    this.getCombination(result, new ArrayList<>(), k, n, 1);
    return result;
  }

  private void getCombination(List<List<Integer>> result, List<Integer> list, int size, int target, int start) {
    if (list.size() > size || target < 0) {
      return;
    } else if (list.size() == size && target == 0) {
      result.add(new ArrayList<>(list));
    } else {
      for (int idx = start; idx < 10; idx++) {
        list.add(idx);
        this.getCombination(result, list, size, target - idx, idx + 1);
        list.remove(list.size() - 1);
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/574620201/){:target="_blank"}

# 설명
1. 주어진 정수인 k 크기의 컬렉션으로 해당 내 값들의 합이 주어진 정수인 n이 되기까지의 조합을 모두 찾는 문제이다.
- 단, 배열 내의 값은 1 ~ 9 까지의 숫자만 허용이 된다.

2. 결과를 넣을 컬렉션인 result를 선언하고, 새 컬렉션을 정의하여 result에 크기가 k이고, 합이 n인 조합을 모두 넣어준다.
- list의 크기가 size를 초과하고 target이 0보다 작으면, 주어진 문제의 결과의 대상이 되지 않으므로 무시한다.
- list의 크기가 size와 동일하고 target이 0과 같으면, 주어진 문제의 결과의 대상이 되므로, result에 새 컬렉션을 정의하여 넣어준다.
- 그 외의 경우는 주어진 문제의 결과를 구하기 위한 과정이므로, start부터 10 미만까지 반복하여 탐색을 진행한다.
  - list에 idx 값을 넣어주고, 재귀 호출을 이용하여 target에 $target - idx$값을, start에 $idx + 1$을 넣어 결과 탐색을 계속 진행한다.
  - 재귀 호출이 끝나면, 마지막으로 넣어준 idx 값을 제거하기 위해 list의 마지막 값을 제거해주고 반복을 계속 진행한다.

3. 합이 n이 되기 위한 k크기의 조합을 모두 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CombinationSumIII.java){:target="_blank"}에서 확인 가능합니다.