---
title: "Leetcode Java Design Underground System"
excerpt: "Leetcode Design Underground System Java"
last_modified_at: 2023-05-31T20:05:00
header:
  image: /assets/images/leetcode/design-underground-system.png
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
[Link](https://leetcode.com/problems/design-underground-system){:target="_blank"}

# 코드
```java
import java.util.AbstractMap;

class UndergroundSystem {

  private Map<Integer, Map.Entry<String, Integer>> travel;
  private Map<Map.Entry<String, String>, Map.Entry<Double, Integer>> averageTime;

  public UndergroundSystem() {
    this.travel = new HashMap<>();
    this.averageTime = new HashMap<>();
  }

  public void checkIn(int id, String stationName, int t) {
    this.travel.putIfAbsent(id, new AbstractMap.SimpleEntry<>(stationName, t));
  }

  public void checkOut(int id, String stationName, int t) {
    if (!this.travel.containsKey(id)) {
      return;
    }
    Map.Entry<String, Integer> prev = this.travel.remove(id);
    Map.Entry<String, String> station = new AbstractMap.SimpleEntry<>(prev.getKey(), stationName);
    double time = t - prev.getValue();
    if (this.averageTime.containsKey(station)) {
      Map.Entry<Double, Integer> curr = this.averageTime.get(station);
      this.averageTime.put(station, new AbstractMap.SimpleEntry<>(curr.getKey() + time, curr.getValue() + 1));
    } else {
      this.averageTime.put(station, new AbstractMap.SimpleEntry<>(time, 1));
    }
  }

  public double getAverageTime(String startStation, String endStation) {
    Map.Entry<Double, Integer> curr = this.averageTime.get(new AbstractMap.SimpleEntry<>(startStation, endStation));
    return curr.getKey() / curr.getValue();
  }

}

/**
 * Your UndergroundSystem object will be instantiated and called as such:
 * UndergroundSystem obj = new UndergroundSystem();
 * obj.checkIn(id,stationName,t);
 * obj.checkOut(id,stationName,t);
 * double param_3 = obj.getAverageTime(startStation,endStation);
 */
```

# 결과
[Link](https://leetcode.com/problems/design-underground-system/submissions/960878486/){:target="_blank"}

# 설명
1. 역에서 다른 역까지 이동하는데 걸리는 평균 시간을 계산하는 UndergroundSystem 클래스를 완성하는 문제이다.
- 메서드인 checkIn(int id, String stationName, int t)은 고객 id로 t시간에 stationName에서 체크인한다.
- 메서드인 checkOut(int id, String stationName, int t)은 고객 id로 t시간에 stationName에서 체크아웃한다.
- 메서드인 getAverageTime(String startStation, String endStation)은 지금까지 고객들 중 startStation에서 endStation까지 걸린 평균 시간을 반환한다. 단, startStation의 시간인 t1은 endStation의 시간인 t2보다 커야 startStation에서 endStation으로 이동한 것으로 간주한다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- travel은 고객이 이동한 기록을 저장하는 변수이다.
- averageTime은 한 역에서 다른 역으로 이동한 총 시간과 횟수를 저장하기 위한 변수이다.

3. 생성자인 UndergroundSystem()를 이용하여 travel과 averageTime을 HashMap으로 초기화한다.

4. 메서드인 checkIn(int id, String stationName, int t)을 정의한다.
- travel에 id에 해당하는 값이 없는 경우, id가 key인 값에 stationName과 t를 [AbstractMap.SimpleEntry](https://docs.oracle.com/javase/8/docs/api/java/util/AbstractMap.SimpleEntry.html){:target="_blank"}를 이용하여 쌍으로 넣어준다.

5. 메서드인 checkOut(int id, String stationName, int t)을 정의한다.
- travel에 id에 해당하는 값이 없는 경우, 체크인한 기록이 없으므로 수행을 멈춘다.
- prve에 travel에서 id에 해당하는 값인 이전 출입한 기록을 제거하여 넣어준다.
- station에 prev의 key인 체크인한 역의 이름과 체크아웃한 주어진 stationName을 쌓으로 넣어준다.
- time에 t와 prev의 값인 체크인한 시간의 차이를 실수 형태로 넣어준다.
- averageTime에 station에 해당하는 값이 존재하면 averageTime의 station에 해당하는 값에 걸린 시간인 time을 더하고 횟수를 증가시켜 넣어준다.
- averageTime에 station에 해당하는 값이 존재하지 않으면 averageTime의 station에 해당하는 값에 time과 1을 쌍으로 넣어준다.

6. 메서드인 getAverageTime(String startStation, String endStation)을 정의한다.
- averageTime에서 startStation에서 endStation까지의 총 걸린 시간과 이동 횟수를 가져와 두 값을 나눈 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DesignUndergroundSystem.java){:target="_blank"}에서 확인 가능합니다.