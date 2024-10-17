---
title: "Leetcode Java Pyramid Transition Matrix"
excerpt: "Leetcode - 'Pyramid Transition Matrix' 문제 Java 풀이"
last_modified_at: 2022-12-09T11:30:00
header:
  image: /assets/images/leetcode/pyramid-transition-matrix.png
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
[Link](https://leetcode.com/problems/pyramid-transition-matrix){:target="_blank"}

# 코드
```java
class Solution {

  public boolean pyramidTransition(String bottom, List<String> allowed) {
    Map<String, List<Character>> map = new HashMap<>();
    for (String s : allowed) {
      String key = s.substring(0, 2);
      map.putIfAbsent(key, new ArrayList<>());
      map.get(key).add(s.charAt(2));
    }
    return this.dfs(map, bottom + "&", new HashSet<>());
  }

  private boolean dfs(Map<String, List<Character>> map, String s, Set<String> set) {
    if (s.length() == 1) {
      return true;
    }
    if (set.contains(s)) {
      return false;
    }
    String prefix = s.substring(0, 2);
    if (prefix.charAt(1) == '&') {
      return this.dfs(map, s.substring(2) + '&', set);
    }
    for (char c : map.getOrDefault(prefix, new ArrayList<>())) {
      if (this.dfs(map, s.substring(1) + c, set)) {
        return true;
      }
    }
    set.add(s);
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/pyramid-transition-matrix/submissions/856891528/){:target="_blank"}

# 설명
1. 가장 밑 바닥이 bottom으로 시작하는 피라미드를 allowed 내 삼각형을 이용하여 완성 가능한지 검증하는 문제이다.
- allowed[i] = "ABC"인 경우, 좌측의 "A"와 우측의 "B" 블록 위에 "C" 블록이 있는 삼각형을 나타낸다.

2. 삼각형의 패턴을 저장할 map을 HashMap으로 초기화 하고, allowed의 모든 값을 이용하여 앞의 두 문자가 키이고 삼각형의 윗 블록인 마지막 문자가 값으로 넣어준다.

3. 4번에서 정의한 dfs(Map<String, List<Character>> map, String s, Set<String> set) 메서드에 위의 map과 bottom에 피라미드 층간 구분 기호인 '&', 새 HashMap을 이용하여 수행한 결과를 주어진 문제의 결과로 반환한다.

4. DFS 방식으로 피라미드가 완성 가능한지 검증하기 위한 dfs(Map<String, List<Character>> map, String s, Set<String> set) 메서드를 정의한다.
- s의 길이가 1인 경우, 구분 기호인 '&'인 경우이므로 true를 반환한다.
- set에 s가 포함된 경우, 이미 포함되지 않는 것으로 검증된 패턴이므로 false를 반환한다.
- prefix에 s의 앞 두 문자열을 넣어준다.
- prefix의 두 번째 문자가 구분 기호인 '&'인 경우, s의 앞 두 문자를 제거하고 '&' 구분 문자를 붙여 재귀 호출한 겨로가를 반환한다.
- map의 prefix의 값을 가져와 c에 각각 넣어 아래를 반복한다.
  - s의 첫 문자를 제거하고 c를 붙여 재귀 호출한 결과가 true인 경우, 피라미드에 포함되는 문자열 이므로 true를 반환한다.
- 위의 수행에 포함되지 않으면 s를 set에 넣어 피라미드에 포함되지 않는 문자열임을 저장한 후, false를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PyramidTransitionMatrix.java){:target="_blank"}에서 확인 가능합니다.