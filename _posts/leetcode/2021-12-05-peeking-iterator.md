---
title: "Leetcode Java Peeking Iterator"
excerpt: "Leetcode Peeking Iterator Java 풀이"
last_modified_at: 2021-12-05T10:00:00
header:
  image: /assets/images/leetcode/peeking-iterator.png
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
[Link](https://leetcode.com/problems/peeking-iterator/){:target="_blank"}

# 코드
```java
//Java Iterator interface reference:
//https://docs.oracle.com/javase/8/docs/api/java/util/Iterator.html
public class PeekingIterator implements Iterator<Integer> {

  private Iterator<Integer> iterator;
  private Integer peekVal;
  private boolean cached;

  public PeekingIterator(Iterator<Integer> iterator) {
    // initialize any member here.
    this.iterator = iterator;
  }

  // Returns the next element in the iteration without advancing the iterator.
  public Integer peek() {
    if (!this.cached) {
      this.peekVal = this.iterator.next();
      this.cached = true;
    }
    return this.peekVal;
  }

  // hasNext() and next() should behave the same as in the Iterator interface.
  // Override them if needed.
  @Override
  public Integer next() {
    if (this.cached) {
      this.cached = false;
      return this.peekVal;
    }
    return this.iterator.next();
  }

  @Override
  public boolean hasNext() {
    if (this.cached) {
      return true;
    }
    return this.iterator.hasNext();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/597040579/){:target="_blank"}

# 설명
1. peek, hasNext, next 기능을 수행하는 Iterator인 PeekingIterator 클래스를 완성하는 문제이다.
- 생성자인 PeekingIterator(Iterator<Integer> iterator)는 정수의 iterator를 초기화 하는 역할을 수행한다.
- 메서드인 peek()는 iterator의 다음 값을 반환하고 포인터를 그대로 유지한다.
- 메서드인 next()는 iterator의 다음 값을 반환하고 포인터를 움직인다.
- 메서드인 hasNext()는 iterator의 값이 존재하는지 여부를 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- iterator는 생성자를 통해 주입된 iterator 객체의 값을 보관하기 위한 변수이다.
- peekVal은 iterator의 값을 순차적으로 보관하여 반환하기 위한 임시 변수이다.
- cached는 iterator의 값을 peekVal에 임시 보관하였는지 여부를 저장하는 변수이다.

3. 주어진 생성자인 PeekingIterator(Iterator<Integer> iterator)를 완성한다.
- 변수를 통해 주입된 iterator를 전역 변수인 iterator에 저장한다.

4. 주어진 메서드인 peek()를 완성한다.
- cached가 false인 경우, iterator의 다음 값을 peekVal에 넣어주고 cached를 true로 바꾼다.
- peekVal의 값을 반환한다.

5. 주어진 메서드인 next()를 완성한다.
- cached가 true인 경우, cached를 false로 바꿔주고 peekVal의 값을 반환한다.
- cached가 false인 경우, iterator의 다음 값을 반환한다.

6. 주어진 메서드인 hasNext()를 완성한다.
- cached가 true인 경우, true를 반환한다.
- cached가 false인 경우, iterator의 값이 존재하는지 여부인 hasNext()의 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PeekingIterator.java){:target="_blank"}에서 확인 가능합니다.