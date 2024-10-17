---
title: "Leetcode Java Reconstruct Itinerary"
excerpt: "Leetcode - 'Reconstruct Itinerary' 문제 Java 풀이"
last_modified_at: 2022-01-09T19:00:00
header:
  image: /assets/images/leetcode/reconstruct-itinerary.png
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
[Link](https://leetcode.com/problems/reconstruct-itinerary/){:target="_blank"}

# 코드
```java
class Solution {

  private Map<String, Queue<String>> targets = new HashMap<>();
  private List<String> result = new ArrayList<>();

  public List<String> findItinerary(List<List<String>> tickets) {
    for (List<String> ticket : tickets) {
      this.targets.putIfAbsent(ticket.get(0), new PriorityQueue<>());
      this.targets.get(ticket.get(0)).add(ticket.get(1));
    }
    this.recursive("JFK");
    return this.result;
  }

  private void recursive(String departure) {
    while (this.targets.containsKey(departure) && !this.targets.get(departure).isEmpty()) {
      this.recursive(this.targets.get(departure).poll());
    }
    this.result.add(0, departure);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/616168461/){:target="_blank"}

# 설명
1. 주어진 tickets는 [출발지, 목적지] 순의 티켓 정보를 가진 컬렉션으로, 해당 컬렉션을 이용하여 목적지의 문자열이 어휘 순서가 작은 순서대로 여정을 만드는 문제이다.
- 단, 여정의 출발은 "JFK"부터 시작한다.
- 예를 들어, ["JFK", "LGA"]는 ["JFK", "LGB"] 보다 어휘 순서가 작다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- targets는 출발지 별 목적지 정보를 담기 위한 컬렉션이다.
- result는 주어진 여정을 넣기 위한 컬렉션이다.

3. 주어진 tickets를 반복하여 targets를 초기화 한다.
- targets에 ticket의 첫 번째 값인 출발지가 존재하지 않는 경우, 해당 값으로 targets에 새 PriorityQueue를 넣어준다.
- targets 내 ticket의 첫 번째 값인 출발지가 Key인 값에 ticket의 두 번째 값인 목적지를 넣어준다.

4. targets의 departure 값이 존재하고, targets의 departure의 값이 비어있지 않을 때 까지 아래를 수행한다.
- targets의 departure의 값 중 첫 값을 빼서 재귀 호출을 수행한다.

5. 4번의 재귀 호출이 끝나면 result의 첫 값에 departure를 추가한다.

6. 4, 5번을 통해서 목적지의 문자열이 어휘 순서가 작은 순서대로의 여정을 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReconstructItinerary.java){:target="_blank"}에서 확인 가능합니다.