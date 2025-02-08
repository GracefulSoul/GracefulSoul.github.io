---
title: "Leetcode Java Design a Number Container System"
excerpt: "Leetcode - 'Design a Number Container System' 문제 Java 풀이"
last_modified_at: 2025-02-08T13:00:00
header:
  image: /assets/images/leetcode/design-a-number-container-system.png
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
[Link](https://leetcode.com/problems/design-a-number-container-system/){:target="_blank"}

# 코드
```java
class NumberContainers {

  private Map<Integer, Integer> indexMap;
  private Map<Integer, TreeSet<Integer>> valueMap;

  public NumberContainers() {
    this.indexMap = new HashMap<>();
    this.valueMap = new HashMap<>();
  }

  public void change(int index, int number) {
    this.indexMap.put(index, number);
    this.valueMap.computeIfAbsent(number, value -> new TreeSet<Integer>()).add(index);
  }

  public int find(int number) {
    if (this.valueMap.containsKey(number)) {
      for (Integer value : this.valueMap.get(number)) {
        if (this.indexMap.get(value) == number) {
          return value;
        }
      }
    }
    return -1;
  }

}

/**
 * Your NumberContainers object will be instantiated and called as such:
 * NumberContainers obj = new NumberContainers();
 * obj.change(index,number);
 * int param_2 = obj.find(number);
 */
```

# 결과
[Link](https://leetcode.com/problems/design-a-number-container-system/submissions/1535362698/){:target="_blank"}

# 설명
1. 아래의 기능을 제공하는 객체를 설계하는 문제이다.
- 생성자인 NumberContainers()는 객체를 초기화한다.
- 메서드인 change(int index, int number)는 특정 index에 number를 넣어준다. 단, 값이 존재하면 기존 값을 덮어쓴다.
- 메서드인 find(int number)는 number에 해당하는 index를 반환한다. 단, number에 해당하는 index가 존재하지 않으면 -1을 반환한다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- indexMap은 index에 대한 number를 저장하기 위한 변수이다.
- valueMap은 number에 해당하는 index를 저정하기 위한 변수이다.

3. 생성자인 NumberContainers()를 정의한다.
- 전역 변수로 정의한 indexMap와 valueMap을 HashMap으로 초기화한다.

4. 메서드인 change(int index, int number)를 정의한다.
- indexMap의 index가 키인 값을 number로 넣어준다.
- valueMap의 number에 해당하는 값이 없으면 새 TreeSet을, 있으면 기존 TreeSet을 가져와 index를 넣어준다.

5. 메서드인 find(int number)를 정의한다.
- valueMap에 number가 존재하는 경우, valueMap의 number에 해당하는 TreeSet을 가져와 순차적으로 작은 값부터 value에 넣어 아래를 반복한다.
  - indexMap에서 value에 해당하는 값이 number와 동일한 경우, value를 주어진 문제의 결과로 반환한다.
- number에 해당하는 index가 존재하지 않으므로 -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DesignANumberContainerSystem.java){:target="_blank"}에서 확인 가능합니다.