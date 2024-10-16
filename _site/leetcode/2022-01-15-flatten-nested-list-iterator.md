---
title: "Leetcode Java Flatten Nested List Iterator"
excerpt: "Leetcode Flatten Nested List Iterator Java 풀이"
last_modified_at: 2022-01-15T12:00:00
header:
  image: /assets/images/leetcode/flatten-nested-list-iterator.png
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
[Link](https://leetcode.com/problems/flatten-nested-list-iterator/){:target="_blank"}

# 코드
```java
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer, rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds, if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds, if it holds a nested list
 *     // Return empty list if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
public class NestedIterator implements Iterator<Integer> {

  private LinkedList<Iterator<NestedInteger>> linkedList;
  private Iterator<NestedInteger> currentIterator;
  private Integer next;

  public NestedIterator(List<NestedInteger> nestedList) {
    this.linkedList = new LinkedList<>();
    this.currentIterator = nestedList.iterator();
    this.next = this.getNext();
  }

  @Override
  public Integer next() {
    Integer temp = next;
    this.next = this.getNext();
    return temp;
  }

  @Override
  public boolean hasNext() {
    return this.next != null;
  }

  private Integer getNext() {
    while (!this.currentIterator.hasNext()) {
      if (this.linkedList.isEmpty()) {
        return null;
      }
      this.currentIterator = this.linkedList.removeLast();
    }
    NestedInteger nextInteger = this.currentIterator.next();
    if (nextInteger.isInteger()) {
      return nextInteger.getInteger();
    }
    this.linkedList.addLast(this.currentIterator);
    this.currentIterator = nextInteger.getList().iterator();
    return this.getNext();
  }

}

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i = new NestedIterator(nestedList);
 * while (i.hasNext()) v[f()] = i.next();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/620004661/){:target="_blank"}

# 설명
1. 중첩된 정수 List인 nestedList를 평면화 시키는 NestedIterator 클래스를 완성하는 문제이다.
- 생성자인 NestedIterator(List<NestedInteger> nestedList)는 nestedList를 이용하여 NestedIterator를 초기화시킨다.
- 메서드인 next()는 평면화된 nestedList의 다음 정수를 반환한다.
- 메서드인 hasNext()는 평면화된 nestedList의 다음 정수가 존재하는지 여부를 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- linkedList는 nestedList를 이용하여 순차적인 정수 활용을 위한 LinkedList이다.
- currentIterator는 linkedList에서 순차적으로 Iterator를 받아와 사용하기 위한 Iterator이다.
- next는 다음 값을 임시 저장하기 위한 정수이다.

3. 순차적으로 정수를 활용하기 위한 getNext() 메서드를 정의한다.
- currentIterator의 다음 값이 없을 때 까지 아래의 경우를 반복한다.
  - linkedList가 비어있을 경우 더 이상 반환시킬 정수가 없으므로, null을 반환한다.
  - 위의 경우가 아닌 경우, currentIterator에 linkedList의 마지막 Iterator를 꺼내 넣어준다. 
- nextInteger에 currentInterator의 다음 차례 NestedInteger를 넣어준다.
- 만일 nextInteger가 Integer형인 경우, nextInteger의 Integer를 반환한다.
- 그렇지 않은 경우 아래를 수행한다.
  - linkedList에 currentIterator를 마지막으로 넣어준다.
  - currentIterator에 nextInteger의 List를 Iterator로 변환하여 넣어준다.
  - 재귀 호출을 수행하여 다음 값을 탐색한다. 

4. 생성자인 NestedIterator(List<NestedInteger> nestedList)를 완성한다.
- linkedList에 새 LinkedList를 정의하여 넣어준다.
- currentIterator에 nestedList를 Iterator로 변환하여 넣어준다.
- next에 3번에서 정의한 getNext() 메서드를 호출한 결과를 넣어준다.

5. 메서드인 next()를 완성한다.
- next의 값을 temp에 임시 보관하고, next에 3번에서 정의한 getNext()의 수행 결과를 넣어준다.
- 임시 저장한 다음 정수인 temp를 반환한다.

6. 메서드인 hasNext()를 완성한다.
- 다음 정수를 저장한 next의 값이 null이면 다음 값이 존재하므로 true를, null이 아니면 다음 값이 존재하지 않으므로 false를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FlattenNestedListIterator.java){:target="_blank"}에서 확인 가능합니다.