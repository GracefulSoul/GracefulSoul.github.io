---
title: "Leetcode Java Insert Delete GetRandom O(1) - Duplicates allowed"
excerpt: "Leetcode Insert Delete GetRandom O(1) - Duplicates allowed Java 풀이"
last_modified_at: 2022-02-09T18:00:00
header:
  image: /assets/images/leetcode/insert-delete-getrandom-o1-duplicates-allowed.png
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
[Link](https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/){:target="_blank"}

# 코드
```java
class RandomizedCollection {

  private Map<Integer, Set<Integer>> map;
  private List<Integer> list;
  private Random random;

  public RandomizedCollection() {
    this.map = new HashMap<>();
    this.list = new ArrayList<>();
    this.random = new Random();
  }

  public boolean insert(int val) {
    boolean isContains = this.map.containsKey(val);
    if (!isContains) {
      this.map.put(val, new HashSet<Integer>());
    }
    this.map.get(val).add(this.list.size());
    this.list.add(val);
    return !isContains;
  }

  public boolean remove(int val) {
    boolean isContains = this.map.containsKey(val);
    if (isContains) {
      int index = this.map.get(val).iterator().next();
      int lastIndex = this.list.size() - 1;
      int num = this.list.get(lastIndex);
      this.list.set(index, num);
      this.map.get(val).remove(index);
      this.map.get(num).add(index);
      this.map.get(num).remove(lastIndex);
      this.list.remove(lastIndex);
      if (this.map.get(val).isEmpty()) {
        this.map.remove(val);
      }
    }
    return isContains;
  }

  public int getRandom() {
    return this.list.get(this.random.nextInt(this.list.size()));
  }

}

/**
 * Your RandomizedCollection object will be instantiated and called as such:
 * RandomizedCollection obj = new RandomizedCollection();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/637772714/){:target="_blank"}

# 설명
1. 지난번 [Insert Delete GetRandom O(1)](../insert-delete-getrandom-o1){:target="_blank"}와 유사한 문제로, 주어진 RandomizedCollection 클래스를 완성하는 문제이다.
- 앞의 문제와 차이점은 중복이 허용된 객체라는 점이다.
- 생성자인 RandomizedCollection()는 RandomizedCollection 객체를 초기화하는 역할을 수행한다.
- 메서드인 insert(int val)는 val 값이 RandomizedCollection 객체 내 존재하지 않았으면  false를, 존재하였다면 true를 반환하면서 val 값을 저장한다.
- 메서드인 remove(int val)는 val 값이 RandomizedCollection 객체 내 존재하면 true를, 존재하지 않았으면 false를 반환하면서 val 값을 제거한다.
- 메서드인 getRandom()는 RandomizedCollection 객체 내 존재하는 값들을 동일한 확률로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 입력된 값을 저장해서 존재하는지 여부를 판단하기 위한 Map이다.
- list는 입력된 값들을 중복되지 않게 저장하기 위한 List이다.
- random은 객체 내 존재하는 값을 임의 확률로 반환하기 위한 객체이다.

3. 생성자인 RandomizedSet()를 완성한다.
- map에 HashMap, list에 ArrayList, random에 Random 객체로 초기화 시켜준다.

4. 메서드인 insert(int val)를 완성한다.
- isContains에 map에 val 값이 존재하는지 여부를 저장한다.
- isContains가 false인 경우 기존에 입력된 값이 존재하지 않았으므로, map의 val 키에 새 HashMap을 넣어준다.
- map의 val이 키로 가진 Set을 꺼내와 list의 크기를 넣어준다.
- list에 val 값을 넣어 값을 계속 이어준다.
- isContains의 반대가 존재 여부이므로 반대 값을 반환한다.

5. 메서드인 remove(int val)를 완성한다.
- isContains에 map에 val 값이 존재하는지 여부를 저장한다.
- isContains가 true인 경우 아래를 수행한다.
  - index에 map의 val이 키인 Set 내 다음 값을 꺼내 넣어준다..
  - lastIndex에 list의 크기의 1 작은 값인 list에 존재하는 마지막 값의 위치로 초기화한다.
  - num에 list의 lastIndex번째 위치인 마지막 값을 꺼내 초기화한다.
  - list의 index번째 위치에 num을 넣어준다.
  - map의 val이 키인 Set에 index를 제거해 list 내 존재하는 위치를 삭제해준다.
  - map의 num이 키인 Set에 index를 넣어 list 내 존재하는 위치를 갱신한다.
  - map의 num이 키인 Set에서 lastIndex번째 값을 제거한다.
  - list의 latIndex에 해당하는 값을 제거한다.
  - map에서 val이 키인 Set이 비어있는 경우, 해당 키를 제거한다.
- isContains의 여부에 따라 삭제를 수행하였으므로, 해당 값을 반환한다..

6. 메서드인 getRandom()를 완성한다.
- list에서 list의 크기 만큼의 임의의 위치 값을 꺼내 반환한다.
  - [Random 객체의 nextInt(int bound) 메서드](https://docs.oracle.com/javase/8/docs/api/java/util/Random.html#nextInt-int-){:target="_blank"}는 0부터 bound 미만까지의 임의 정수 숫자열을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/InsertDeleteGetRandomO1.java){:target="_blank"}에서 확인 가능합니다.