---
title: "Leetcode Java Evaluate Division"
excerpt: "Leetcode Evaluate Division Java 풀이"
last_modified_at: 2022-02-27T12:00:00
header:
  image: /assets/images/leetcode/evaluate-division.png
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
[Link](https://leetcode.com/problems/evaluate-division/){:target="_blank"}

# 코드
```java
class Solution {

  public double[] calcEquation(List<List<String>> equations, double[] values, List<List<String>> queries) {
    Map<String, Map<String, Double>> map = new HashMap<>();
    for (int idx = 0; idx < values.length; idx++) {
      List<String> equation = equations.get(idx);
      map.putIfAbsent(equation.get(0), new HashMap<>());
      map.putIfAbsent(equation.get(1), new HashMap<>());
      map.get(equation.get(0)).put(equation.get(1), values[idx]);
      map.get(equation.get(1)).put(equation.get(0), 1 / values[idx]);
    }
    double[] result = new double[queries.size()];
    for (int idx = 0; idx < queries.size(); idx++) {
      List<String> query = queries.get(idx);
      result[idx] = this.dfs(query.get(0), query.get(1), 1, map, new HashSet<>());
    }
    return result;
  }

  private double dfs(String s, String t, double num, Map<String, Map<String, Double>> map, Set<String> set) {
    if (!map.containsKey(s) || !set.add(s)) {
      return -1;
    } else if (s.equals(t)) {
      return num;
    } else {
      Map<String, Double> next = map.get(s);
      for (String str : next.keySet()) {
        double result = this.dfs(str, t, num * next.get(str), map, set);
        if (result != -1) {
          return result;
        }
      }
      return -1;
    }
  }

}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int param_1 = obj.pick(target);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/649555553/){:target="_blank"}

# 설명
1. 쌍으로 이루어진 문자열 List인 equations과 숫자 List인 values가 주어지면, query의 계산 결과를 구하는 문제이다.
- $equations[i] = [Ai, Bi]$일 때, $Ai / Bi = values[i]$를 만족한다.
- $queries[j] = [Cj, Dj]$일 때, $Cj / Dj = result[i]$를 만족하는 값들을 구한다.
- 단, 값을 유추할 수 없는 경우 -1.0을 반환한다.

2. equations와 values를 엮어 저장 할 map을 HashMap으로 초기화한다.

3. 0부터 values의 갯수 이전까지 idx를 증가시키며 map에 값을 넣어준다.
- equations의 idx번째 List를 equation에 임시로 넣어준다.
- equations의 각 값들이 key가되는 value가 map에 존재하지 않을 경우, 새 HashMap을 넣어준다.
- map에서 equation의 첫 번째 값이 key인 Map을 꺼내와서, equation의 두 번째 값과 values의 idx번째 값을 key와 value로 엮어 넣어준다.
- map에서 equation의 두 번째 값이 key인 Map을 꺼내와서, equation의 첫 번째 값과 values의 idx번째 값을 1로 나눈 결과를 key와 value로 엮어 넣어준다.

4. 결과를 저장할 result 배열을 queries의 갯수의 크기로 초기화한다.

5. 0부터 queries의 갯수 이전까지 idx를 증가시키며 result에 값을 넣어준다.
- queries의 idx번째 List를 query에 넣어준다.
- result의 idx번째 값에 6번에서 정의한 dfs(Map<String, Map<String, Double>> map, Set<String> set, String q1, String q2, double num) 메서드의 수행 결과를 넣어준다.

6. result에 값을 넣기 위한 dfs(Map<String, Map<String, Double>> map, Set<String> set, String q1, String q2, double num) 메서드를 정의한다.
- map에 q1이 존재하지 않거나 set에 q1이 존재하지 않는 경우 결과를 판단할 수 없으므로, -1을 반환한다.
- q1과 q2가 동일한 경우 두 값의 나눈 값은 1이므로, num을 그대로 반환한다.
- map에서 q1에 해당하는 Map을 next에 넣어주고 아래를 수행한다.
  - next의 keySet을 str로 반복을 수행하여 str과 q2, num에 next의 str이 key인 값의 값을 가져와 곱하여 재귀 호출을 수행하여 -1이 아닌 경우, 해당 값을 반환한다.
  - 반복이 정상적으로 완료되면 유추 가능한 값이 존재하지 않는다는 의미이므로, -1을 반환한다.

7. 5번의 반복이 완료되면 결과를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/EvaluateDivision.java){:target="_blank"}에서 확인 가능합니다.