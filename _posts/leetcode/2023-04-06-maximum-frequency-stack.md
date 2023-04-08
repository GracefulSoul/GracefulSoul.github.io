---
title: "Leetcode Java Maximum Frequency Stack"
excerpt: "Leetcode Maximum Frequency Stack Java"
last_modified_at: 2023-04-06T20:20:00
header:
  image: /assets/images/leetcode/maximum-frequency-stack.png
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
[Link](https://leetcode.com/problems/maximum-frequency-stack){:target="_blank"}

# 코드
```java
class FreqStack {

  private int max;
  private Map<Integer, Integer> frequencyMap;
  private List<Deque<Integer>> valList;

  public FreqStack() {
    this.max = 0;
    this.frequencyMap = new HashMap<>();
    this.valList = new ArrayList<>();
  }

  public void push(int val) {
    int frequency = this.frequencyMap.getOrDefault(val, 0) + 1;
    this.frequencyMap.put(val, frequency);
    this.max = Math.max(this.max, frequency);
    if (frequency > this.valList.size()) {
      this.valList.add(new ArrayDeque<>());
    }
    this.valList.get(frequency - 1).push(val);
  }

  public int pop() {
    int val = this.valList.get(this.valList.size() - 1).pop();
    if (this.max == 1) {
      this.frequencyMap.remove(val);
    } else {
      this.frequencyMap.replace(val, this.max - 1);
    }
    if (this.valList.get(this.valList.size() - 1).isEmpty()) {
      this.valList.remove(this.valList.size() - 1);
      this.max--;
    }
    return val;
  }

}

/**
 * Your FreqStack object will be instantiated and called as such:
 * FreqStack obj = new FreqStack();
 * obj.push(val);
 * int param_2 = obj.pop();
 */
```

# 결과
[Link](https://leetcode.com/problems/maximum-frequency-stack/submissions/929005726/){:target="_blank"}

# 설명
1. 주어진 값을 스택에 넣고, 스택에서 가장 많이 발생한 값을 반환하는 FreqStack 클래스를 완성하는 문제이다.
- 생성자인 FreqStack()는 주어진 데이터 구조를 초기화하는 역할을 수행한다.
- 메서드인 push(int val)는 주어진 값을 스택에 값을 넣는 역할을 수행한다.
- 메서드인 pop()은 스택에서 가장 많이 발생한 값을 스택에서 제거하고 반환하고, 동일하게 발생한 값이 여럿일 경우 먼저 들어온 스택의 top에 가까운 값을 제거하면서 반환한다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- max은 최대 발생 횟수를 저장할 변수이다.
- frequencyMap은 숫자 별 발생 횟수를 키와 값으로 저장할 변수이다.
- valList는 발생 횟수에 해당하는 값을 저장할 변수이다.

3. 생성자인 FreqStack()을 정의한다.
- max에 초기 횟수인 0을 넣어 초기화한다.
- frequencyMap은 키와 값으로 저장하기 위해 HashMap으로 초기화한다.
- valList는 발생 횟수 별 값을 저장하기 위해 ArrayList로 초기화한다.

4. 메서드인 push(int val)를 정의한다.
- frequency에 frequencyMap에서 val에 해당하는 발생 횟수를, 없으면 0을 가져와 1을 더해서 넣어준다.
- frequencyMap에 val에 해당하는 발생 횟수인 frequency로 바꿔준다.
- max에 max와 frequency 중 큰 값을 넣어 많이 발생한 횟수를 갱신한다.
- frequency가 valList의 크기보다 큰 경우, valList에 ArrayDeque를 새로 생성하여 넣어준다.
- valList의 $frequency - 1$번째의 ArrayDeque에 val을 넣어준다.

5. 메서드인 메서드인 pop()을 정의한다.
- val에 valList에서 가장 많이 발생한 위치의 값 중 top에 가까운 값을 꺼내준다.
- max가 1인 한 번만 발생한 값인 경우, frequencyMap에서 해당 값의 발생 횟수를 제거한다.
- max가 1이 아니면 frequencyMap에서 해당 값의 발생 횟수를 차감한다.
- valList의 가장 많이 발생한 위치의 ArrayDeque가 비어있는 경우, 해당 ArrayDeque를 제거하고 max를 차감한다.
- 마지막으로 임시 저장한 val을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumFrequencyStack.java){:target="_blank"}에서 확인 가능합니다.