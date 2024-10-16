---
title: "Leetcode Java Positions of Large Groups"
excerpt: "Leetcode Positions of Large Groups Java"
last_modified_at: 2023-02-06T19:10:00
header:
  image: /assets/images/leetcode/positions-of-large-groups.png
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
[Link](https://leetcode.com/problems/positions-of-large-groups){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> largeGroupPositions(String s) {
    List<List<Integer>> list = new ArrayList<>();
    char[] charArray = s.toCharArray();
    int start = 0;
    for (int idx = 1; idx < s.length(); idx++) {
      List<Integer> temp = new ArrayList<>();
      while (idx < s.length() && charArray[idx - 1] == charArray[idx]) {
        idx++;
      }
      if (idx - start >= 3) {
        temp.add(start);
        temp.add(idx - 1);
        list.add(temp);
      }
      start = idx;
    }
    return list;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/positions-of-large-groups/submissions/892563981/){:target="_blank"}

# 설명
1. s 내 3번 이상 반복된 문자열의 시작 위치와 종료 위치를 모아 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- list는 결과를 넣을 변수로, ArrayList로 초기화한다.
- start는 문자열의 시작 위치를 임시 저장할 변수로, 첫 위치인 0으로 초기화한다.

3. 1부터 s의 길이 미만까지 idx를 증가시키며 아래를 수행한다.
- temp는 문자열의 시작 위치와 종료 위치를 저장할 변수로, ArrayList로 초기화한다.
- idx가 s의 길이 미만이고, $idx - 1$번째 문자와 idx번째 문자가 동일하면 idx를 계속 증가시킨다.
- $idx - start$가 3 이상인 세 번 이상 반복된 문자열인 경우, [start, $idx - 1$]을 list에 넣어준다.
- start에 idx를 넣고 반복을 계속 수행한다.

4. 반복이 완료되면 3번 이상 반복된 문자의 위치 값들이 저장된 list를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PositionsOfLargeGroups.java){:target="_blank"}에서 확인 가능합니다.