---
title: "Leetcode Java All O`one Data Structure"
excerpt: "Leetcode All O`one Data Structure Java 풀이"
last_modified_at: 2022-03-25T12:00:00
header:
  image: /assets/images/leetcode/all-oone-data-structure.png
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
[Link](https://leetcode.com/problems/all-oone-data-structure/){:target="_blank"}

# 코드
```java
class AllOne {

	private Node head;
	private Node tail;
	private Map<String, Node> map;

	public AllOne() {
		this.map = new HashMap<>();
	}

	public void inc(String key) {
		Node node = this.map.get(key);
		if (node == null) {
			node = new Node(key);
			this.map.put(key, node);
			if (this.head == null) {
				this.head = node;
				this.tail = node;
			} else {
				this.head.left = node;
				node.right = this.head;
				this.head = node;
			}
		} else {
			node.count++;
			while (this.tail != node && node.count > node.right.count) {
				this.swap(node, node.right);
			}
		}
	}

	public void dec(String key) {
		Node node = this.map.get(key);
		node.count--;
		if (node.count == 0) {
			this.map.remove(key);
			if (node.right != null) {
				node.right.left = node.left;
			}
			if (node.left != null) {
				node.left.right = node.right;
			}
			if (node == head) {
				this.head = node.right;
			}
			if (node == tail) {
				this.tail = node.left;
			}
		} else {
			while (this.head != node && node.count < node.left.count) {
				this.swap(node.left, node);
			}
		}
	}

	public String getMinKey() {
		return this.head == null ? "" : this.head.val; 
	}

	public String getMaxKey() {
		return this.tail == null ? "" : this.tail.val;
	}

	private void swap(Node node1, Node node2) {
		Node left = node1.left;
		Node right = node2.right;
		if (left == null) {
			this.head = node2;
		} else {
			left.right = node2;
		}
		node2.left = left;
		if (right == null) {
			this.tail = node1;
		} else {
			right.left = node1;
		}
		node1.right = right;
		node1.left = node2;
		node2.right = node1;
	}

}

class Node {

	public String val;
	public int count;
	public Node left;
	public Node right;

	public Node() {
	}

	public Node(String val) {
		this.val = val;
		this.count = 1;
	}

}

/**
 * Your AllOne object will be instantiated and called as such:
 * AllOne obj = new AllOne();
 * obj.inc(key);
 * obj.dec(key);
 * String param_3 = obj.getMaxKey();
 * String param_4 = obj.getMinKey();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/666736764/){:target="_blank"}

# 설명
1. 문자열의 갯수를 저장하고, 최소 및 최대 갯수의 문자열을 반환하는 기능을 가진 데이터 구조를 설계한다.
- 생성자인 AllOne()는 객체를 초기화한다.
- 메서드인 inc(String key)는 key에 해당하는 갯수를 증가시키고, 데이터 구조에 key가 존재하지 않는다면 key를 추가하고 갯수를 1로 설정한다.
- 메서드인 dec(String key)는 key에 해당하는 갯수를 감소시키고, 갯수가 0인 경우 데이터 구조에서 제거한다.
  - 단, key가 감소하기 전에 데이터 구조에 존재한다는 가정을 전제로 둔다.
- 메서드인 getMaxKey()는 최대 갯수의 key들 중 하나를 반환하고, key가 존재하지 않는 경우 공백("")을 반환한다.
- 메서드인 getMinKey()는 최소 갯수의 key들 중 하나를 반환하고, key가 존재하지 않는 경우 공백("")을 반환한다.

2. 문자열과 저장된 횟수를 활용하기 위한 Node 객체를 정의한다.
- val은 문자열을 저장하기 위한 변수이다.
- count는 저장 횟수를 남길 변수이다.
- left는 count가 큰 val에 해당하는 Node를 이어줄 변수이다.
- right는 count가 작은 val에 해당하는 Node를 이어줄 변수이다.

3. 문제 풀이에 필요한 변수를 정의한다.
- head는 최대 갯수의 문자열을 가진 Node를 보관할 변수이다.
- tail은 최소 갯수의 문자열을 가진 Node를 보관할 변수이다.
- map은 key에 대한 Node를 저장하여 Node에서 탐색하는 것보다 빠르게 횟수를 찾기 위한 변수이다.

4. 생성자인 AllOne()를 정의한다.
- Node를 임시 저장할 map을 HashMap으로 초기화한다.

5. 메서드인 inc(String key)와 dec(String key)를 수행하며 node의 순서를 바꾸어줄 swap(Node node1, Node node2) 메서드를 정의한다.
- left에 node1의 left 노드를, right에 node2의 right 노드를 넣어준다.
- left가 null인지 확인하여 아래를 수행한다.
  - null인 경우 node1이 최소 횟수의 문자열을 가진 Node이므로, head에 node2를 넣어준다.
  - null이 아닌 경우, left의 right 노드에 node2를 넣어 이어준다.
- node2의 left 노드에 left를 넣어준다.
- right가 null인지 확인하여 아래를 수행한다.
  - null인 경우 node2가 최대 횟수의 문자열을 가진 Node이므로, tail에 node1을 넣어준다.
  - null이 아닌 경우, left의 right 노드에 node1을 넣어 이어준다.
- node2 -> node1 순으로 정렬시키기 위해 순서를 바꾸어 이어준다.

6. 메서드인 inc(String key)를 정의한다.
- map에서 key에 해당하는 Node를 찾아 node에 넣어준다.
- node가 없을 경우 key가 처음 입력된 문자열이므로, 아래를 수행한다.
  - node에 key가 val이고 count가 1인 Node를 만들어 넣어준다.
  - map에 key를 이용하여 node를 넣어준다.
  - head가 null인 경우 객체 초기화 후 처음 입력된 값이므로, head와 tail에 node를 넣어준다.
  - head가 null이 아니면 기존 입력된 값들이 있으므로, Node의 순서를 node 다음 head가 되도록 순서를 바꾸어 head에 node를 넣어준다.
- node가 존재하는 경우, 아래를 수행하여 순서를 바꿔준다.
  - node의 count를 증가하고 node가 tail이 아니고 node의 count가 right 노드의 count보다 클 때 까지 반복하여, 5번의 swap(Node node1, Node node2) 메서드로 node와 node의 right 노드의 순서를 계속 바꾸어준다.

7. 메서드인 dec(String key)를 정의한다.
- map에서 key에 해당하는 Node를 찾아 node에 넣어준다.
- node의 count를 감소시킨다.
  - 기존 전제 하에 dec(String key) 메서드를 호출하는 경우, key에 해당하는 node가 존재하므로 node가 null이 될 수 없어 null 여부를 확인하지 않는다.
- node의 count가 0인 경우 해당 노드를 제거해야 하므로, 아래를 수행한다.
  - map에서 key에 해당하는 노드를 제거한다.
  - node의 right 노드가 존재하는 경우, node의 right 노드의 left 노드에 node의 left 노드를 넣어 node를 배제하고 이어준다.
  - node의 left 노드가 존재하는 경우, node의 left 노드의 right 노드에 node의 right 노드를 넣어 node를 배제하고 이어준다.
  - node가 head인 경우, head에 node의 right 노드를 넣어 node 다음의 작은 횟수의 문자열을 가진 노드를 head에 설정한다.
  - node가 tail인 경우, tail에 node의 left 노드를 넣어 node 다음의 큰 횟수의 문자열을 가진 노드를 tail에 설정한다.
- node의 count가 1 이상인 경우, 아래를 수행하여 순서를 바꿔준다.
  - head가 node가 아니고 node의 count가 node의 left 노드의 count보다 작을 때 까지 반복하여, 5번의 swap(Node node1, Node node2) 메서드로 node의 left 노드와 node를 계속 바꾸어준다.

8. 메서드인 getMinKey()를 정의한다.
- head가 null인 경우 ""를, 아니면 head의 val 값을 반환한다.

9. 메서드인 getMaxKey()를 정의한다.
- tail이 null인 경우 ""를, 아니면 tail의 val 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AllOoneDataStructure.java){:target="_blank"}에서 확인 가능합니다.