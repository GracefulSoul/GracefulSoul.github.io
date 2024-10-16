---
title: "Leetcode Java Online Stock Span"
excerpt: "Leetcode Online Stock Span Java"
last_modified_at: 2023-04-15T15:00:00
header:
  image: /assets/images/leetcode/online-stock-span.png
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
[Link](https://leetcode.com/problems/online-stock-span){:target="_blank"}

# 코드
```java
class StockSpanner {

  private Stack<int[]> stack;

  public StockSpanner() {
    this.stack = new Stack<>();
  }

  public int next(int price) {
    int span = 1;
    while (!this.stack.isEmpty() && price >= this.stack.peek()[0]) {
      span += this.stack.pop()[1];
    }
    this.stack.push(new int[] { price, span });
    return span;
  }

}

/**
 * Your StockSpanner object will be instantiated and called as such:
 * StockSpanner obj = new StockSpanner();
 * int param_1 = obj.next(price);
 */
```

# 결과
[Link](https://leetcode.com/problems/online-stock-span/submissions/933962595/){:target="_blank"}

# 설명
1. 일부 주식에 대한 일일 가격을 수집하고, 해당 주식의 현재 가격 범위를 반환하는 StockSpanner 클래스를 완성하는 문제이다.
- 생성자인 StockSpanner()는 StockSpanner 객체를 초기화한다.
- 메서드인 next(int price)는 주식의 오늘의 가격이 price와 동일한 경우, 현재 가격 범위를 반환한다.

2. stack은 일일 가격 범위를 저장하기 위한 변수이다.

3. 생성자인 StockSpanner()를 완성한다.
- stack을 새 Stack으로 초기화한다.

4. 메서드인 next(int price)를 완성한다.
- span은 주식의 가격 범위를 저장할 변수로, 1로 초기화한다.
- stack이 비어있지 않으면서 price가 stack의 마지막 값의 가격보다 크거나 같으면 span에 stack의 마지막 값의 범위를 넣어준다.
- 반복이 완료되면 price와 span을 배열로 stack에 넣어 범위를 저장해주고 span을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/OnlineStockSpan.java){:target="_blank"}에서 확인 가능합니다.