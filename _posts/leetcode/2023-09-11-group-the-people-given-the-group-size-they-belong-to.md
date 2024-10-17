---
title: "Leetcode Java Group the People Given the Group Size They Belong To"
excerpt: "Leetcode Medium - 'Group the People Given the Group Size They Belong To' 문제 Java 풀이"
last_modified_at: 2023-09-11T18:40:00
header:
  image: /assets/images/leetcode/group-the-people-given-the-group-size-they-belong-to.png
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
[Link](https://leetcode.com/problems/group-the-people-given-the-group-size-they-belong-to){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> groupThePeople(int[] groupSizes) {
    List<List<Integer>> result = new ArrayList<>();
    Map<Integer, List<Integer>> groups = new HashMap<>();
    for (int i = 0; i < groupSizes.length; i++) {
      List<Integer> list = groups.computeIfAbsent(groupSizes[i], k -> new ArrayList<>());
      list.add(i);
      if (list.size() == groupSizes[i]) {
        result.add(list);
        groups.put(groupSizes[i], new ArrayList<>());
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/group-the-people-given-the-group-size-they-belong-to/submissions/1046389823/){:target="_blank"}

# 설명
1. groupSizes를 이용하여 아래의 규칙을 만족하도록 구성하여 반환하는 문제이다.
- groupSizes[i]의 값은 i번째 사람이 정확히 해당 값만큼의 크기의 그룹에 속해야 한다.
- 각 사람은 한 집단에 속하며, 여러 개의 답이 있으면 그 중 하나를 반환하면 된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 그룹 별 인원들을 담을 변수로, ArrayList로 초기화한다.
- groups는 각 그룹을 저장할 변수로, HashMap으로 초기화한다.

3. 0부터 groupSizes의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- list에 groups 내 키가 groupSizes[i] 번째 값을 꺼내 넣어주고, 해당 값이 존재하지 않으면 새 ArrayList를 넣어준다.
- list에 i를 넣어 그룹을 지어준다.
- list의 길이가 groupSizes[i]의 값과 동일한 경우, result에 list를 넣고 gruops에 gruopSizes[i]번째 위치에 ArrayList를 넣어 새 그룹으로 초기화한다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/GroupThePeopleGivenTheGroupSizeTheyBelongTo.java){:target="_blank"}에서 확인 가능합니다.