---
title: "Leetcode Java Design HashSet"
excerpt: "Leetcode Design HashSet Java"
last_modified_at: 2022-10-27T19:30:00
header:
  image: /assets/images/leetcode/design-hashset.png
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
[Link](https://leetcode.com/problems/design-hashset){:target="_blank"}

# 코드
```java
class MyHashSet {

  private boolean[] set;

  public MyHashSet() {
    this.set = new boolean[10];
  }

  public void add(int key) {
    if (key >= this.set.length) {
      this.set = Arrays.copyOf(this.set, key + 1);
    }
    this.set[key] = true;
  }

  public boolean contains(int key) {
    if (key >= this.set.length) {
      return false;
    } else {
      return this.set[key];
    }
  }

  public void remove(int key) {
    if (key < this.set.length) {
      this.set[key] = false;
    }
  }

}

/**
 * Your MyHashSet object will be instantiated and called as such:
 * MyHashSet obj = new MyHashSet();
 * obj.add(key);
 * obj.remove(key);
 * boolean param_3 = obj.contains(key);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/831982910/){:target="_blank"}

# 설명
1. HashSet과 동일한 기능인 MyHashSet을 구현하는 문제이다.
- 생성자인 MyHashSet()은 객체를 초기화한다.
- 메서드인 add(key)는 HashSet 내 key를 저장한다.
- 메서드인 contains(key)는 HashSet 내 key가 있는지 검증 결과를 반환한다.
- 메서드인 remove(key)는 HashSet 내 key를 제거한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- set은 key가 추가되었는지 검증하기 위한 배열이다.

3. 생성자인 MyHashSet()을 완성한다.
- set을 임시로 10 크기의 배열로 초기화한다.

4. 메서드인 add(key)를 완성한다.
- set의 길이보다 key가 더 크거나 같은 경우, set의 크기를 key가 들어갈 수 있도록 $key + 1$ 크기로 확장한다.
- key의 값이 포함되었다는 의미로 set의 key번째 자리의 값을 true로 바꾸어준다.

5. 메서드인 contains(key)를 완성한다.
- set의 길이보다 key가 더 크거나 같은 경우, set의 key번째 자리 결과를 반환한다.
- 위의 경우가 아니라면 해당 값이 추가된 적이 없으므로, false를 반환한다.

6. 메서드인 remove(key)를 완성한다.
- set의 길이가 key보다 큰 경우, key의 값을 제거한다는 의미로 set의 key번째 위치의 값을 false로 바꾸어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DesignHashSet.java){:target="_blank"}에서 확인 가능합니다.