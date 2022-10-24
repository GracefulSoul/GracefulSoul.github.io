---
title: "Leetcode Java Kth Largest Element in a Stream"
excerpt: "Leetcode Kth Largest Element in a Stream Java"
last_modified_at: 2022-10-24T20:30:00
header:
  image: /assets/images/leetcode/kth-largest-element-in-a-stream.png
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
[Link](https://leetcode.com/problems/kth-largest-element-in-a-stream){:target="_blank"}

# 코드
```java
class KthLargest {

	private Queue<Integer> queue;
	private int k;

	public KthLargest(int k, int[] nums) {
		this.k = k;
		this.queue = new PriorityQueue<Integer>(k);
		for (int num : nums) {
			this.add(num);
		}
	}

	public int add(int val) {
		this.queue.offer(val);
		if (this.queue.size() > k) {
			this.queue.poll();
		}
		return this.queue.peek();
	}

}

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest obj = new KthLargest(k, nums);
 * int param_1 = obj.add(val);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/829222163/){:target="_blank"}

# 설명
1. k번째로 큰 값을 반환하는 스트림 객체를 만드는 문제이다.
- 생성자인 KthLargest(int k, int[] nums)는 k번째 큰 값을 찾을 k와 초기 스트림인 nums를 이용하여 객체를 초기화한다.
- 메서드인 add(int val)는 val 값을 스트림에 넣어주고, k번째 큰 값을 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- queue는 스트림의 값들을 차례대로 저장할 변수이다.
- k는 스트림의 k번째 큰 값을 저장할 변수이다.

3. 생성자인 KthLargest(int k, int[] nums)를 완성한다.
- k에 주어진 k를 넣어 저장한다.
- queue에 k번째 큰 값을 유지하기 위해 k 크기의 PriorityQueue로 초기화한다.

4. 메서드인 add(int val)를 완성한다.
- queue에 val 값을 넣어준다.
- queue의 크기가 k를 초과하는 경우, 가장 앞의 큰 값을 꺼내준다.
- qeuue의 맨 앞의 값은 k번째로 큰 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KthLargestElementInAStream.java){:target="_blank"}에서 확인 가능합니다.