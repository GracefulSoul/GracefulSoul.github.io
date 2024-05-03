---
title: "Leetcode Java Brace Expansion II"
excerpt: "Leetcode Brace Expansion II Java"
last_modified_at: 2024-05-03T19:40:00
header:
  image: /assets/images/leetcode/brace-expansion-ii.png
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
[Link](https://leetcode.com/problems/brace-expansion-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> braceExpansionII(String expression) {
    return this.dfs(expression.toCharArray(), 0, expression.length() - 1);
  }

  private List<String> dfs(char[] expression, int start, int end) {
    Set<String> result = new TreeSet<>();
    List<List<String>> groups = new ArrayList<>();
    groups.add(new ArrayList<>());
    int count = 0;
    for (int i = 0, j = start; j <= end; j++) {
      if (expression[j] == '{' && ++count == 1) {
        i = j + 1;
      } else if (expression[j] == '}' && --count == 0) {
        this.merge(groups, this.dfs(expression, i, j - 1));
      } else if (count == 0) {
        if (expression[j] == ',') {
          groups.add(new ArrayList<>());
        } else {
          this.merge(groups, new ArrayList<>(Arrays.asList(String.valueOf(expression[j]))));
        }
      }
    }
    for (List<String> group : groups) {
      for (String word : group) {
        result.add(word);
      }
    }
    return new ArrayList<>(result);
  }

  private void merge(List<List<String>> groups, List<String> group) {
    List<String> temp = groups.get(groups.size() - 1);
    if (temp.isEmpty()) {
      groups.set(groups.size() - 1, group);
    } else {
      List<String> result = new ArrayList<>();
      for (String s1 : temp) {
        for (String s2 : group) {
          result.add(s1 + s2);
        }
      }
      groups.set(groups.size() - 1, result);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/largest-positive-integer-that-exists-with-its-negative/submissions/1247262016/){:target="_blank"}

# 설명
1. 주어진 expression로 아래의 R(expr) 표현식을 이용하여 나타낼 수 있는 문자열을 오름차순으로 정렬하여 반환하는 문제이다.
- 단일 문자가 들어간 경우는 아래의 결과로 표현된다.
  - R("a") = {"a"}
  - R("w") = {"w"}
- 콤마로 구분된 두 개 이상의 값들로 이루어진 집합인 경우 아래의 결과로 표현된다.
  - R("{a,b,c}") = {"a","b","c"}
- 두 집합을 다시 묶어진 집합은 각 집합 내 최대 하나의 문자들만 포함된 집합으로 표현된다.
  - R("{{a,b},{b,c}}") = {"a","b","c"}, 
- 두 집합을 표현식으로 표현하면 두 문자들의 조합으로 표현된다.
  - R("{a,b}{c,d}") = {"ac","ad","bc","bd"}
- 위 경우들이 포함된 표현식은 아래와 같이 표현된다.
  - R("a{b,c}{d,e}f{g,h}") = {"abdfg", "abdfh", "abefg", "abefh", "acdfg", "acdfh", "acefg", "acefh"}

2. 3번에서 정의한 dfs(char[] expression, int start, int end)에 expression의 문자 배열, 처음 시작인 0, 마지막 위치인 expression의 길이보다 1 작은 값을 각각 넣어 수행한 결과를 주어진 문제의 결과로 반환한다.

3. DFS 방식으로 결과를 탐색할 dfs(char[] expression, int start, int end) 메서드를 완성한다.
- 결과를 탐색하기 위한 변수를 정의한다.
  - result는 결과를 중복 제거된 사전 순서순으로 저장할 변수로, TreeSet으로 초기화한다.
  - groups는 가능한 문자열들을 순차적으로 저장할 변수로, ArrayList로 초기화한다.
  - count는 중괄호('{}')의 갯수를 저장할 변수로, 0으로 초기화한다.
- start부터 end 이하까지 j를 증가시키고 i를 0으로 초기화시켜 아래를 반복한다.
  - expression[j]의 값이 중괄호의 시작 문자('{')이면서 count를 증가시킨 값이 1인 경우, i에 $j + 1$을 넣어준다.
  - expression[j]의 값이 중괄호의 종료 문자('}')이면서 count를 감소시킨 값이 0인 경우, 4번에서 정의한 merge(List<List<String>> groups, List<String> group) 메서드에 groups와 i부터 $j - 1$까지 재귀 호출한 결과를 넣어 수행한다.
  - count가 0이면서 expression[j]의 값이 ','인 연결 문자열인 경우, groups에 새 조합을 저장하기위해서 ArrayList를 초기화하여 넣어준다.
  - count가 0이면서 expression[j]의 값이 일반 문자열인 경우, 4번에서 정의한 merge(List<List<String>> groups, List<String> group) 메서드에 groups와 expression[j]의 값을 새 ArrayList에 넣어 수행한다.
- 위의 반복이 완료되면 groups의 값을 순차적으로 group에 넣고, group의 값들을 순차적으로 word에 넣어 result에 넣어 ArrayList로 변환한 값을 반환한다.

4. groups 내 값들을 R(expr) 표현식과 같이 넣어줄 merge(List<List<String>> groups, List<String> group) 메서드를 정의한다.
- temp에 groups의 마지막 ArrayList를 넣어준다.
- temp가 비어있는 배열인 경우, 마지막 위치에 group을 넣어준다.
- 위의 경우가 아니라면 마지막 위치에 temp와 group의 값들을 각각 순차적으로 연결하여 신규 ArrayList에 넣어 groups의 마지막 위치에 넣어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BraceExpansionII.java){:target="_blank"}에서 확인 가능합니다.