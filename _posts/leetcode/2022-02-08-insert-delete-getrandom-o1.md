---
title: "Leetcode Java Insert Delete GetRandom O(1)"
excerpt: "Leetcode Insert Delete GetRandom O(1) Java 풀이"
last_modified_at: 2022-02-08T13:00:00
header:
  image: /assets/images/leetcode/insert-delete-getrandom-o1.png
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
[Link](https://leetcode.com/problems/insert-delete-getrandom-o1/){:target="_blank"}

# 코드
```java
class RandomizedSet {

  private Map<Integer, Integer> map;
  private List<Integer> list;
  private Random random = new Random();

  public RandomizedSet() {
    this.map = new HashMap<>();
    this.list = new ArrayList<>();
  }

  public boolean insert(int val) {
    if (this.map.containsKey(val)) {
      return false;
    } else {
      this.map.put(val, this.list.size());
      this.list.add(val);
      return true;
    }
  }

  public boolean remove(int val) {
    if (this.map.containsKey(val)) {
      int index = this.map.get(val);
      int lastIndex = this.list.size() - 1;
      int num = this.list.get(lastIndex);
      this.list.set(index, num);
      this.map.put(num, index);
      this.map.remove(val);
      this.list.remove(lastIndex);
      return true;
    } else {
      return false;
    }
  }

  public int getRandom() {
    return this.list.get(this.random.nextInt(this.list.size()));
  }

}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/636853342/){:target="_blank"}

# 설명
1. 주어진 RandomizedSet 클래스를 완성하는 문제이다.
- 생성자인 RandomizedSet()는 RandomizedSet 객체를 초기화하는 역할을 수행한다.
- 메서드인 insert(int val)는 val 값이 RandomizedSet 객체 내 존재하지 않았으면 val 값을 저장한 후 false를 반환하고, 존재하였다면 true만 반환한다.
- 메서드인 remove(int val)는 val 값이 RandomizedSet 객체 내 존재하면 val 값을 제거한 후 true를 반환하고, 존재하지 않았으면 false만 반환한다.
- 메서드인 getRandom()는 RandomizedSet 객체 내 존재하는 값들을 동일한 확률로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 입력된 값을 저장해서 존재하는지 여부를 판단하기 위한 Map이다.
- list는 입력된 값들을 중복되지 않게 저장하기 위한 List이다.
- random은 객체 내 존재하는 값을 임의 확률로 반환하기 위한 객체이다.

3. 생성자인 RandomizedSet()를 완성한다.
- map에 HashMap, list에 ArrayList로 초기화 시켜준다.

4. 메서드인 insert(int val)를 완성한다.
- map에 val 값이 존재하는 경우, false를 반환한다.
- map에 val 값이 존재하지 않는 경우, 아래를 수행한다.
  - map의 val이 키인 값에 list의 크기를 넣어준다.
  - list에 val 값을 넣어주고, true를 반환한다.

5. 메서드인 remove(int val)를 완성한다.
- map에 val 값이 존재하는 경우, 아래를 수행한다.
  - index에 map의 val이 키인 값인 list 내 존재하는 위치로 초기화한다.
  - lastIndex에 list의 크기의 1 작은 값인 list에 존재하는 마지막 값의 위치로 초기화한다.
  - num에 list의 lastIndex번째 위치인 마지막 값을 꺼내 초기화한다.
  - list의 index번째 위치에 num을 넣어준다.
  - map의 num이 키인 값에 index를 넣어 list 내 존재하는 위치를 갱신한다.
  - map에서 val인 키와 값을 제거한다.
  - list의 latIndex에 해당하는 값을 제거한다.
- map에 val 값이 존재하지 않는 경우, false를 반환한다.

6. 메서드인 getRandom()를 완성한다.
- list에서 list의 크기 만큼의 임의의 위치 값을 꺼내 반환한다.
  - [Random 객체의 nextInt(int bound) 메서드](https://docs.oracle.com/javase/8/docs/api/java/util/Random.html#nextInt-int-){:target="_blank"}는 0부터 bound 미만까지의 임의 정수 숫자열을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/InsertDeleteGetRandomO1.java){:target="_blank"}에서 확인 가능합니다.