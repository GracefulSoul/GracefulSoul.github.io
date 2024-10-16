---
title: "Leetcode Java Dinner Plate Stacks"
excerpt: "Leetcode Dinner Plate Stacks Java"
last_modified_at: 2024-08-24T18:10:00
header:
  image: /assets/images/leetcode/dinner-plate-stacks.png
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
[Link](https://leetcode.com/problems/dinner-plate-stacks/){:target="_blank"}

# 코드
```java
class DinnerPlates {

  private List<Stack<Integer>> stacks;
  private TreeSet<Integer> treeSet;
  private int capacity;

  public DinnerPlates(int capacity) {
    this.stacks = new ArrayList<>();
    this.treeSet = new TreeSet<>();
    this.capacity = capacity;
  }

  public void push(int val) {
    if (this.treeSet.isEmpty()) {
      this.stacks.add(new Stack<>());
      this.treeSet.add(this.stacks.size() - 1);
    }
    Stack<Integer> stack = this.stacks.get(this.treeSet.first());
    stack.push(val);
    if (stack.size() == this.capacity) {
      this.treeSet.pollFirst();
    }
  }

  public int pop() {
    if (this.stacks.isEmpty()) {
      return -1;
    } else {
      int val = this.stacks.getLast().pop();
      this.treeSet.add(this.stacks.size() - 1);
      while (!this.stacks.isEmpty() && this.stacks.getLast().isEmpty()) {
        this.stacks.removeLast();
        this.treeSet.pollLast();
      }
      return val;
    }
  }

  public int popAtStack(int index) {
    if (index >= this.stacks.size()) {
      return -1;
    } else if (index == this.stacks.size() - 1) {
      return this.pop();
    } else {
      this.treeSet.add(index);
      Stack<Integer> stack = this.stacks.get(index);
      return stack.isEmpty() ? -1 : stack.pop();
    }
  }

}

/**
 * Your DinnerPlates object will be instantiated and called as such:
 * DinnerPlates obj = new DinnerPlates(capacity);
 * obj.push(val);
 * int param_2 = obj.pop();
 * int param_3 = obj.popAtStack(index);
 */
```

# 결과
[Link](https://leetcode.com/problems/dinner-plate-stacks/submissions/1366210106/){:target="_blank"}

# 설명
1. 0부터 좌측에서 우측으로 값을 최대 capacity 만큼 수용 가능한 스택을 무한히 많이 보유한 DinnerPlates 객체를 완성하는 문제이다.
- 생성자인 DinnerPlates(int capacity)는 객체를 초기화 하며 최대 capacity 만큼 수용 가능할 스택을 만들어준다.
- 메서드인 push(int val)는 val 값을 capacity 미만의 값을 보유한 스택에 값을 좌측부터 넣어준다.
- 메서드인 pop()은 가장 처음의 스택에서 오른쪽의 비어있지 않은 값을 꺼내서 반환한다. 단, 값이 존재하지 않으면 -1을 반환한다.
- 메서드인 popAtStack(int index)은 가장 위에 있는 스택에서 index번째 값을 꺼내서 반환한다. 단, 값이 존재하지 않으면 -1을 반환한다.

2. 각 연산에 필요한 전역 변수를 정의한다.
- stacks는 각 스택을 저장할 변수이다.
- treeSet은 각 스택의 크기를 저장할 변수이다.
- capacity는 생성자를 통해 주입되는 스택의 최대 크기를 저장할 변수이다.

3. 생성자인 DinnerPlates(int capacity)를 완성한다.
- stacks에 ArrayList를, treeSet에 TreeSet을, capacity에 주입된 capacity를 넣어준다.

4. 메서드인 push(int val)를 완성한다.
- treeSet이 비어있는 초기 수행인 경우, stacks에 새 Stack을 넣어준 후, treeSet에 현재 스택의 갯수를 저장한다.
- stack에 stacks에서 treeSet의 첫 값에 해당하는 스택을 꺼내 넣어준다.
- stack에 val을 넣어준 후, stack의 크기가 capacity와 동일한 경우, treeSet에 우선 순위가 높은 값을 꺼내 제거한다.

5. 메서드인 pop()을 정의한다.
- stacks가 비어있는 경우, 꺼낼 값이 없으므로 -1을 반환한다.
- 위의 경우가 아니라면 아래를 수행한다.
  - val에 stacks의 마지막 스택의 우선 순위가 높은 값을 꺼내준다.
  - treeSet에 해당 뺀 값을 제외한 현재 스택의 크기를 저장해준다.
  - stacks가 비어있지 않거나 stacks의 마지막 스택이 비어있지 않을 때 까지, stacks의 마지막 스택을 삭제하고 treeSet에서 마지막으로 우선 순위가 낮은 값을 값을 제거하여 빈 스택과 저장된 크기 정보를 삭제한다.
  - val 값을 반환해준다.

6. 메서드인 popAtStack(int index)을 정의한다.
- index가 stacks 크기보다 크거나 같은 경우, 꺼낼 수 없으므로 -1을 반환한다.
- 위의 경우가 아니면서 index가 stacks의 마지막 위치인 경우, 5번의 pop() 메서드를 수행한다.
- 위의 모든 경우가 아니라면 아래를 수행한다.
  - treeSet에 index를 추가하여 신규 스택의 위치인 꺼낸 값의 위치를 저장해준다.
  - stack에 stacks에서 index번째 스택을 꺼내 넣어준다.
  - stack이 버이었으면 -1을, 아니면 마지막 값을 꺼내 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DinnerPlateStacks.java){:target="_blank"}에서 확인 가능합니다.