---
title: "Leetcode Java Range Module"
excerpt: "Leetcode Range Module Java"
last_modified_at: 2022-11-05T11:20:00
header:
  image: /assets/images/leetcode/range-module.png
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
[Link](https://leetcode.com/problems/range-module){:target="_blank"}

# 코드
```java
class RangeModule {

  private TreeMap<Integer, Integer> map;

  public RangeModule() {
    this.map = new TreeMap<>();
  }

  public void addRange(int left, int right) {
    Integer start = this.map.floorKey(left);
    Integer end = this.map.floorKey(right);
    if (start != null && this.map.get(start) >= left) {
      left = start;
    }
    if (end != null && this.map.get(end) > right) {
      right = this.map.get(end);
    }
    this.map.put(left, right);
    this.map.subMap(left, false, right, true).clear();
  }

  public boolean queryRange(int left, int right) {
    Integer start = this.map.floorKey(left);
    if (start == null) {
      return false;
    } else {
      return this.map.get(start) >= right;
    }
  }

  public void removeRange(int left, int right) {
    Integer start = this.map.floorKey(left);
    Integer end = this.map.floorKey(right);
    if (end != null && this.map.get(end) > right) {
      this.map.put(right, this.map.get(end));
    }
    if (start != null && this.map.get(start) > left) {
      this.map.put(start, left);
    }
    this.map.subMap(left, true, right, false).clear();
  }

}

/**
 * Your RangeModule object will be instantiated and called as such:
 * RangeModule obj = new RangeModule();
 * obj.addRange(left,right);
 * boolean param_2 = obj.queryRange(left,right);
 * obj.removeRange(left,right);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/837119051/){:target="_blank"}

# 설명
1. 반 열린 구간으로 표현하고, 이에 대한 쿼리할 데이터 구조인 Range Module을 설계하는 문제이다.
- 생성자인 RangeModule()은 데이터 구조를 초기화한다.
- 메서드인 addRange(int left, int right)는 반 열린 구간인 [left, right)를 추가하고, 기존에 존재하는 간격과 부분적으로 겹치는 경우 해당 구간을 추가한다.
- 메서드인 queryRange(int left, int right)는 [left, right) 범위가 현재 범위에 포함되면 true를 반환하고, 아니면 false를 반환한다.
- 메서드인 removeRange(int left, int right)는 반 열린 구간인 [left, right)를 현재 범위에서 제거한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 구간을 저장하기 위해 이진 트리 기반으로 저장할 TreeMap으로 정의한다.

3. 생성자인 RangeModule()을 완성한다.
- 전역 변수로 정의한 map을 TreeMap으로 초기화한다.

4. 메서드인 addRange(int left, int right)를 완성한다.
- start와 end에 map에서 각각 left, right와 같거나 작은 값 중 가장 큰 키 값을 넣어준다.
- start가 null이거나 map에서 start에 해당하는 값이 left보다 크거나 같은 경우, left에 start를 넣어준다.
- end가 null이거나 map에서 end에 해당하는 값이 right보다 큰 경우, right에 map에서 end에 해당하는 값을 넣어준다.
- map에 left에 해당하는 값에 right를 넣어 확장된 [left, right) 구간을 저장해준다.
- 위에서 추가된 값에 포함된 map에 left 초과부터 right 이하까지 값들을 모두 제거한다. 

5. 메서드인 queryRange(int left, int right)를 완성한다.
- start에 map에서 left와 같거나 작은 값 중 가장 큰 키 값을 넣어준다.
- start가 null인 경우, 구간 시작에 대한 결과가 없으므로 false를 주어진 문제의 결과로 반환한다.
- start가 null이 아닌 경우, map의 start에 해당하는 값이 right보다 크거나 같은지 여부를 반환한다.

6. 메서드인 removeRange(int left, int right)를 완성한다.
- start와 end에 map에서 각각 left, right와 같거나 작은 값 중 가장 큰 키 값을 넣어준다.
- end가 null이거나 map에서 end에 해당하는 값이 right보다 큰 경우, map에 right가 키인 값에 map에 end가 키인 값을 넣어준다.
- start가 null이거나 map에서 start에 해당하는 값이 left보다 크거나 같은 경우, map에 start가 키인 값에 left를 넣어준다.
- map에 left 이상부터 right 미만까지 해당하는 값들을 모두 제거한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RangeModule.java){:target="_blank"}에서 확인 가능합니다.