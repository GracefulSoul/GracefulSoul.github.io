---
title: "Leetcode Java Find Median from Data Stream"
excerpt: "Leetcode Find Median from Data Stream Java 풀이"
last_modified_at: 2021-12-10T12:00:00
header:
  image: /assets/images/leetcode/find-median-from-data-stream.png
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
[Link](https://leetcode.com/problems/find-median-from-data-stream/){:target="_blank"}

# 코드
```java
class MedianFinder {

  private Queue<Integer> queue;
  private Queue<Integer> reverse;
  private boolean isEven;

  public MedianFinder() {
    this.queue = new PriorityQueue<>();
    this.reverse = new PriorityQueue<>((a, b) -> b - a);
    this.isEven = true;
  }

  public void addNum(int num) {
    if (this.isEven) {
      this.queue.add(num);
      this.reverse.add(this.queue.poll());
    } else {
      this.reverse.add(num);
      this.queue.add(this.reverse.poll());
    }
    this.isEven = !this.isEven;
  }

  public double findMedian() {
    if (this.isEven) {
      return (this.queue.peek() + this.reverse.peek()) / 2.0;
    } else {
      return this.reverse.peek();
    }
  }

}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/599609758/){:target="_blank"}

# 설명
1. addNum을 통해 주입된 숫자를 이용하여 findMedian으로 중앙값을 출력하는 MedianFinder 클래스를 완성하는 문제이다.
- 생성자인 MedianFinder()는 MedianFinder 클래스를 초기화시킨다.
- 메서드인 addNum(int num)은 주어진 정수 num을 데이터 구조에 맞는 흐름에 넣어준다.
- 메서드인 findMedian()은 주어진 정수들을 이용하여 중앙값을 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- queue는 주어진 정수를 순차적인 순서로 저장하는 역할로, 주어진 정수들의 초반의 절반 값들을 저장하는 큐이다.
- reverse는 주어진 정수를 역순으로 저장하는 역할로, 주어진 정수들의 절반 이후의 값들을 저장하는 큐이다.
- isEven은 주어진 정수의 개수가 짝수인지 여부를 저장하는 변수이다.

3. 주어진 생성자인 MedianFinder()를 완성한다.
- queue와 reverse를 순서대로 정의하기 위해 PriorityQueue로 초기화 하고, reverse의 경우 순서를 내림차순으로 저장해야 하므로 (a, b) -> (b - a)를 넣어준다.
- isEven은 현재 주어진 정수가 없으므로 true로 초기화한다.

4. 주어진 메서드인 addNum(int num)을 완성한다.
- isEven이 true인 짝수번째로 입력된 숫자의 경우, queue에 주어진 정수 num을 넣고 reverse에 queue의 가장 큰 값을 꺼내서 넣어준다.
- isEven이 false인 홀수번쨰 입력된 숫자인 경우, reverse에 주어진 정수 num을 넣고, queue에 reverse의 가장 작은 값을 꺼내서 넣어준다.
- isEven에 isEven의 값의 반대 값을 넣어준다.

5. 주어진 메서드인 findMedian()을 완성한다.
- isEven이 true인 주어진 정수가 짝수개라면, queue의 가장 작은 값과 reverse의 가장 큰 값을 꺼내 Double형인 2.0으로 나눈 결과를 반환한다.
- isEven이 false인 주어진 정수가 홀수개라면, reverse의 가장 큰 값을 꺼내 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindMedianFromDataStream.java){:target="_blank"}에서 확인 가능합니다.