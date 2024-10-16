---
title: "Leetcode Java Time Based Key-Value Store"
excerpt: "Leetcode Time Based Key-Value Store Java"
last_modified_at: 2023-08-24T18:45:00
header:
  image: /assets/images/leetcode/time-based-key-value-store.png
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
[Link](https://leetcode.com/problems/time-based-key-value-store){:target="_blank"}

# 코드
```java
class TimeMap {

  private Map<String, List<Pair>> map;

  public TimeMap() {
    this.map = new HashMap<>();
  }

  public void set(String key, String value, int timestamp) {
    if (!this.map.containsKey(key)) {
      this.map.put(key, new ArrayList<>());
    }
    this.map.get(key).add(new Pair(value, timestamp));
  }

  public String get(String key, int timestamp) {
    if (!this.map.containsKey(key)) {
      return "";
    } else {
      return this.binarySearch(this.map.get(key), timestamp);
    }
  }

  protected String binarySearch(List<Pair> list, int timestamp) {
    int left = 0;
    int right = list.size() - 1;
    while (left < right) {
      int mid = (left + right + 1) >> 1;
      if (list.get(mid).timestamp <= timestamp) {
        left = mid;
      } else {
        right = mid - 1;
      }
    }
    return list.get(left).timestamp <= timestamp ? list.get(left).value : "";
  }

}

class Pair {

  String value;
  int timestamp;

  public Pair(String value, int timestamp) {
    this.value = value;
    this.timestamp = timestamp;
  }

}

/**
 * Your TimeMap object will be instantiated and called as such:
 * TimeMap obj = new TimeMap();
 * obj.set(key,value,timestamp);
 * String param_2 = obj.get(key,timestamp);
 */
```

# 결과
[Link](https://leetcode.com/problems/time-based-key-value-store/submissions/1030382892/){:target="_blank"}

# 설명
1. 서로 다른 타임스탬프에서 동일한 키에 대해 여러 값을 저장하고 특정 타임스탬프에서 키의 값을 검색할 수 있는 키-값 데이터 구조인 TreeMap을 정의하는 문제이다.
- 생성자인 TimeMap()는 데이터 구조를 초기화한다.
- 메서드인 set(String key, String value, int timestamp)은 key와 value를 주어진 timestamp에 저장한다.
- 메서드인 get(String key, int timestamp)은 timestamp 이전에 저장한 값들 중 key에 해당하는 값을 찾아 반환한다.
  - 조건을 만족하는 여러 값이 존재하는 경우, 가장 큰 timestamp의 값을 반환한다.
  - 해당 값이 존재하지 않으면 ""을 반환한다.

2. value와 timestamp를 쌍으로 엮어서 저장할 Pair 클래스를 정의한다.

3. 전역 변수인 map은 key와 Pair를 저장할 변수이다.

4. 생성자인 TimeMap()을 정의한다.
- 전역 변수인 map을 HashMap으로 초기화한다.

5. 메서드인 set(String key, String value, int timestamp)을 정의한다.
- map에 key가 존재하지 않는다면, key에 ArrayList를 새로 초기화하여 넣어준다.
- map에 key의 List를 꺼내 value와 timestamp로 Pair를 정의하여 넣어준다.

6. 메서드인 get(String key, int timestamp)을 정의한다.
- map에 key가 존재하지 않으면 ""을 반환한다.
- 위의 경우가 아니라면 map에서 key의 값을 꺼내 7번에서 정의한 binarySearch(List<Pair> list, int timestamp) 메서드를 수행한 결과를 넣어준다.

7. 이진 탐색을 수행할 binarySearch(List<Pair> list, int timestamp) 메서드를 정의한다.
- left와 right는 탐색을 수행할 위치 변수로, 0과 list의 마지막 위치 값을 넣어준다.
- left가 right보다 작을 때까지 아래를 수행한다.
  - mid에 $left + right + 1$의 비트를 우측으로 한 칸 이동한 값을 넣어준다.
  - list에 mid번째 Pair의 timestamp가 timestamp보다 작거나 같은 경우, left에 mid를 아니면 right에 $mid - 1$을 넣어준다.
- 반복이 완료되면 list의 left번째 Pair의 timestamp가 timestamp보다 작거나 같으면 해당 값을, 아니면 ""을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TimeBasedKeyValueStore.java){:target="_blank"}에서 확인 가능합니다.