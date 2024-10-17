---
title: "Leetcode Java Design Skiplist"
excerpt: "Leetcode Hard - 'Design Skiplist' 문제 Java 풀이"
last_modified_at: 2024-10-13T10:40:00
header:
  image: /assets/images/leetcode/design-skiplist.png
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
[Link](https://leetcode.com/problems/design-skiplist/){:target="_blank"}

# 코드
```java
class Skiplist {

  private Node head;
  private Random random;

  public Skiplist() {
    this.head = new Node(-1, null, null);
    this.random = new Random();
  }

  public boolean search(int target) {
    Node curr = this.head;
    while (curr != null) {
      while (curr.next != null && curr.next.val < target) {
        curr = curr.next;
      }
      if (curr.next != null && curr.next.val == target) {
        return true;
      }
      curr = curr.down;
    }
    return false;
  }

  public void add(int num) {
    Stack<Node> stack = new Stack<>();
    Node curr = this.head;
    while (curr != null) {
      while (curr.next != null && curr.next.val < num) {
        curr = curr.next;
      }
      stack.push(curr);
      curr = curr.down;
    }
    boolean insert = true;
    Node down = null;
    while (insert && !stack.isEmpty()) {
      curr = stack.pop();
      curr.next = new Node(num, curr.next, down);
      down = curr.next;
      insert = this.random.nextDouble() < 0.5;
    }
    if (insert) {
      this.head = new Node(-1, null, this.head);
    }
  }

  public boolean erase(int num) {
    Node curr = this.head;
    boolean found = false;
    while (curr != null) {
      while (curr.next != null && curr.next.val < num) {
        curr = curr.next;
      }
      if (curr.next != null && curr.next.val == num) {
        found = true;
        curr.next = curr.next.next;
      }
      curr = curr.down;
    }
    return found;
  }

}

class Node {

  public int val;
  public Node next;
  public Node down;

  public Node() {
  }

  public Node(int val) {
    this.val = val;
  }

  public Node(int val, Node next, Node down) {
    this.val = val;
    this.next = next;
    this.down = down;
  }

}
/**
 * Your Skiplist object will be instantiated and called as such:
 * Skiplist obj = new Skiplist();
 * boolean param_1 = obj.search(target);
 * obj.add(num);
 * boolean param_3 = obj.erase(num);
 */
```

# 결과
[Link](https://leetcode.com/problems/design-skiplist/submissions/1420493685/){:target="_blank"}

# 설명
1. 아래의 기능을 만족하는 다중 레이어가 존재하는 Skiplist 객체를 만드는 문제이다.
- 생성자인 Skiplist()는 Skiplist 객체를 초기화한다.
- 메서드인 search(int target)는 target 값이 Skiplist에 존재하는지 유무를 반환한다.
- 메서드인 add(int num)는 Skiplist에 num을 추가한다.
- 메서드인 erase(int num)는 Skiplist에 num을 삭제한 결과를 반환한다. 단, num이 여러 개 존재하는 경우 하나만 삭제해도 괜찮다.

2. 문제 풀이에 필요한 Node 객체를 정의한다.
- val은 현재 노드의 값을 저장한 변수이다.
- next는 다음 노드, down은 다음 계층의 노드를 연결할 변수이다.

3. 문제 풀이에 필요한 전역 변수를 정의한다.
- head는 SkipList를 구성하기 위한 첫 계층의 노드이다.
- random은 계층 생성을 하기 위한 변수이다.

4. 생성자인 Skiplist()를 정의한다.
- head에 값이 -1이고 next와 down이 null인 Node를 생성하여 넣어준다.
- random에 임의 값을 생성하기 위한 Random 객체를 생성하여 넣어준다.

5. 메서드인 search(int target)를 정의한다.
- curr에 SkipList가 구성된 head를 넣어준다.
- curr이 존재할 때 까지 아래를 반복한다.
  - curr의 next 노드가 존재하면서 해당 노드의 val 값이 target 미만일 때 까지, curr에 next 노드를 넣어 다음 노드로 이동한다.
  - curr의 next 노드가 조재하면서 해당 노드가 val 값이 target일 경우, true를 반환한다.
  - curr에 curr의 down 노드인 다음 계층의 노드를 넣어준다.
- 반복이 모두 완료되면 탐색된 값이 없으므로, false를 반환한다.

6. 메서드인 add(int num)를 완성한다.
- 메서드 수행에 필요한 변수를 정의한다.
  - curr에 SkipList가 구성된 head를 넣어준다.
  - stack은 계층별 해당 값의 미만까지 노드를 넣어줄 변수로, curr을 반복하여 각 계층에서 num 이하의 마지막 노드를 stack에 넣어준다.
  - insert는 신규 계층을 생성할지 검증할 변수로, true로 초기화한다.
  - down은 다음 계층 노드를 넣기 위한 변수로, null로 초기화한다.
- insert이면서 stack이 비어있지 않을 때 까지 아래를 반복한다.
  - curr에 stack에서 꺼낸 노드를 넣어준다.
  - curr의 다음 노드에 num, curr의 next 노드, down을 이용하여 새 노드를 생성하여 이어준다.
  - down에 curr의 next를 넣은 후 insert를 확률적으로 다음 계층을 생성할지 여부를 넣어준다.
- insert true인 경우, 신규 노드를 상위 계층으로 추가한다.

7. 메서드인 erase(int num)를 완성한다.
- 메서드 수행에 필요한 변수를 정의한다.
  - curr에 SkipList가 구성된 head를 넣어준다.
  - found는 삭제할 대상을 찾았는지 검증할 변수로, false로 초기화한다.
- curr이 존재할 때 까지 아래를 반복한다.
  - curr의 next 노드가 존재하면서 해당 노드의 val 값이 target 미만일 때 까지, curr에 next 노드를 넣어 다음 노드로 이동한다.
  - curr의 next 노드가 존재하지 않으면서 해당 노드의 val 값이 num과 동일한 경우, found에 true를 넣고 curr의 next 노드에 해당 노드의 next 노드를 넣어 curr의 next 노드를 제거한다.
  - curr에 curr의 down 노드인 다음 계층의 노드를 넣어준다.
- 반복이 완료되었으면 found를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DesignSkiplist.java){:target="_blank"}에서 확인 가능합니다.