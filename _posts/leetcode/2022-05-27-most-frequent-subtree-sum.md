---
title: "Leetcode Java Most Frequent Subtree Sum"
excerpt: "Leetcode Most Frequent Subtree Sum Java"
last_modified_at: 2022-05-27T09:00:00
header:
  image: /assets/images/leetcode/most-frequent-subtree-sum.png
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
[Link](https://leetcode.com/problems/most-frequent-subtree-sum/){:target="_blank"}

# 코드
```java
class Solution {

  private int max = 0;

  public int[] findFrequentTreeSum(TreeNode root) {
    List<Integer> list = new ArrayList<>();
    this.dfs(root, new HashMap<>(), list);
    int[] result = new int[list.size()];
    for (int idx = 0; idx < list.size(); idx++) {
      result[idx] = list.get(idx);
    }
    return result;
  }

  private int dfs(TreeNode root, Map<Integer, Integer> map, List<Integer> list) {
    if (root == null) {
      return 0;
    }
    int sum = root.val + this.dfs(root.left, map, list) + this.dfs(root.right, map, list);
    int frequency = map.getOrDefault(sum, 0) + 1;
    map.put(sum, frequency);
    if (frequency > this.max) {
      max = frequency;
      list.clear();
      list.add(sum);
    } else if (frequency == this.max) {
      list.add(sum);
    }
    return sum;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/707972074/){:target="_blank"}

# 설명
1. root 내 빈도수가 가장 많은 하위 트리의 합계를 반환하는 문제이다.

2. max는 최고 빈도수를 저장할 전역 변수로, 0으로 초기화한다.

3. 빈도수가 가장 많은 하위 트리의 합계를 넣을 list를 정의하고, 새 HashMap과 함께 4번에서 정의한 dfs(TreeNode root, Map<Integer, Integer> map, List<Integer> list) 메서드를 수행한다.

4. DFS 방식으로 root를 탐색하여 list에 결과를 넣어줄 dfs(TreeNode root, Map<Integer, Integer> map, List<Integer> list) 메서드를 정의한다.
- root가 null인 경우, 0을 반환한다.
- sum에 root의 val 값과 left와 right의 TreeNode로 재귀 호출을 수행한 결과를 합쳐준다.
- frequency에 map에서 sum에 해당하는 값을 가져와 1을 더한 값을 저장하고, 다시 해당 값을 넣어준다.
- max보다 frequency가 높은 경우 최고 빈도인 부분 노드가 발생하였으므로, list를 초기화하고 sum을 넣어준다.
- max와 frequency가 같은 경우 동일한 최고 빈도의 부분 노드이므로, list에 sum을 넣어준다.
- 수행이 완료되었으면 sum을 반환한다.

5. list의 값들을 정수 배열로 변환해서 넣을 result 배열을 list 크기로 초기화하고, list의 모든 값들을 result에 넣어준다.

6. 반복이 완료되면 주어진 문제의 결과로 result를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MostFrequentSubtreeSum.java){:target="_blank"}에서 확인 가능합니다.