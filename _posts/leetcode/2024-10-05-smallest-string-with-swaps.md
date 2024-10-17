---
title: "Leetcode Java Smallest String With Swaps"
excerpt: "Leetcode Medium - 'Smallest String With Swaps' 문제 Java 풀이"
last_modified_at: 2024-10-05T10:30:00
header:
  image: /assets/images/leetcode/smallest-string-with-swaps.png
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
[Link](https://leetcode.com/problems/smallest-string-with-swaps/){:target="_blank"}

# 코드
```java
class Solution {

  public String smallestStringWithSwaps(String s, List<List<Integer>> pairs) {
    char[] charArray = s.toCharArray();
    int length = charArray.length;
    int[] parent = new int[length];
    Map<Integer, Queue<Character>> map = new HashMap<>();
    for (int i = 0; i < length; i++) {
      parent[i] = i;
    }
    for (List<Integer> pair : pairs) {
      this.union(parent, pair.get(0), pair.get(1));
    }
    for (int i = 0; i < length; i++) {
      map.computeIfAbsent(this.find(parent, i), k -> new PriorityQueue<>());
      map.get(parent[i]).offer(charArray[i]);
    }
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < length; i++) {
      sb.append(map.get(parent[i]).poll());
    }
    return sb.toString();
  }

  private void union(int[] parent, int i, int j) {
    int pi = this.find(parent, i);
    int pj = this.find(parent, j);
    if (pi > pj) {
      parent[pi] = pj;
    } else {
      parent[pj] = pi;
    }
  }

  private int find(int[] parent, int i) {
    if (i != parent[i]) {
      parent[i] = this.find(parent, parent[i]);
    }
    return parent[i];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/smallest-string-with-swaps/submissions/1412100428/){:target="_blank"}

# 설명
1. s를 pairs 내 임의 순서의 문자 위치를 스왑하여 사전적으로 가장 작은 문자열을 만들어 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray와 length는 s를 문자 배열로 변환한 배열과 길이를 저장한 변수이다.
- parent는 각 위치 별 부모 위치를 저장하기 위한 배열로, length 길이의 정수 배열로 초기화하여 각 자리에 현재 위치를 넣어준다.
- map은 위치 별 가능한 문자들을 저장할 변수로, HashMap으로 초기화한다.

3. pairs를 순차적으로 pair에 넣어 4번에서 정의한 union(int[] parent, int i, int j) 메서드에 parent와 pair의 각 값을 넣어 수행한다.

4. [Union-Find](https://en.wikipedia.org/wiki/Disjoint-set_data_structure#Proof_of_O(m_log*_n)_time_complexity_of_Union-Find){:target="_blank"} 알고리즘으로 문제해결하기 위한 union(int[] parent, int i, int j) 메서드를 정의한다.
- pi와 pj에 5번에서 정의한 find(int[] parent, int i) 메서드를 수행한 결과를 넣어준다.
- pi가 pj보다 큰 경우, parent[pi]에 pj를 아니면 parent[pj]에 pi를 넣어 병합한다.

5. [Union-Find](https://en.wikipedia.org/wiki/Disjoint-set_data_structure#Proof_of_O(m_log*_n)_time_complexity_of_Union-Find){:target="_blank"} 알고리즘으로 문제해결하기 위한 find(int[] parent, int i) 메서드를 정의한다.
- i와 parent[i]가 다른 경우, parent[i]에 parent와 parent[i]로 재귀 호출한 결과인 부모 위치의 값을 넣어준다.
- parent[i]를 반환한다.

6. 0부터 length까지 i를 증가시키며 아래를 수행한다.
- map의 5번에서 정의한 find(int[] parent, int i) 메서드를 수행한 결과에 대한 값이 존재하지 않으면, 오름차순 정렬된 값을 저장할 PriorityQueue를 넣어준다.
- map의 parent[i]에 해당하는 PriorityQueue에 charArray[i]를 넣어 저장한다.

7. 동적으로 결과를 조합할 StringBuilder인 sb를 정의하고, map에서 parent[i]에 해당하는 PriorityQueue의 사전적으로 가장 작은 값인 첫 값을 꺼내 sb에 이어준다.

8. 위의 반복을 통해 완성된 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SmallestStringWithSwaps.java){:target="_blank"}에서 확인 가능합니다.