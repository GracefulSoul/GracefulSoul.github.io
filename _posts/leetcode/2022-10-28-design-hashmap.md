---
title: "Leetcode Java Design HashMap"
excerpt: "Leetcode Design HashMap Java"
last_modified_at: 2022-10-28T19:00:00
header:
  image: /assets/images/leetcode/design-hashmap.png
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
[Link](https://leetcode.com/problems/design-hashmap){:target="_blank"}

# 코드
```java
class MyHashMap {

  private int[] map;

  public MyHashMap() {
    this.map = new int[10];
  }

  public void put(int key, int value) {
    if (key >= this.map.length) {
      this.map = Arrays.copyOf(this.map, key + 1);
    }
    this.map[key] = value == 0 ? -1 : value;
  }

  public int get(int key) {
    if (key >= this.map.length || this.map[key] == 0) {
      return -1;
    } else {
      return this.map[key] == -1 ? 0 : this.map[key];
    }
  }

  public void remove(int key) {
    if (key < this.map.length) {
      this.map[key] = 0;
    }
  }

}

/**
 * Your MyHashMap object will be instantiated and called as such:
 * MyHashMap obj = new MyHashMap();
 * obj.put(key,value);
 * int param_2 = obj.get(key);
 * obj.remove(key);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/831981955/){:target="_blank"}

# 설명
1. HashMap과 동일한 기능인 MyHashMap을 구현하는 문제이다.
- 생성자인 MyHashMap()은 객체를 초기화한다.
- 메서드인 put(int key, int value)은 HashMap 내 key의 값에 value를 저장한다. 단, 동일한 key에 값이 존재한다면 value로 값을 바꾸어준다.
- 메서드인 get(key)는 HashMap 내 key의 값을 반환한다.
- 메서드인 remove(key)는 HashMap 내 key의 값을 제거한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 key번째 value를 저장하기 위한 배열이다.

3. 생성자인 MyHashSet()을 완성한다.
- map을 임시로 10 크기의 배열로 초기화한다.

4. 메서드인 put(int key, int value)을 완성한다.
- map의 길이보다 key가 더 크거나 같은 경우, map의 크기를 key가 들어갈 수 있도록 $key + 1$ 크기로 확장한다.
- map의 key번째 자리의 값에 value가 0인 경우 -1을 넣어 0이 들어간 것을 표시해주고, 아니면 value를 그대로 넣어준다.

5. 메서드인 get(key)를 완성한다.
- map의 길이보다 key가 더 크거나 같거나 map의 key번째 자리의 값이 0인 경우, 값이 존재하지 않으므로 -1을 반환한다.
- 위의 경우가 아니라면 map의 key번째 자리가 -1인 경우 0을 추가한 경우이므로 0을, 아니면 해당 값 그대로 반환한다.

6. 메서드인 remove(key)를 완성한다.
- map의 길이가 key보다 큰 경우, key의 값을 0을 넣어 초기화한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DesignHashMap.java){:target="_blank"}에서 확인 가능합니다.