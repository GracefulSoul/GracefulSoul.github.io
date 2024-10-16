---
title: "Leetcode Java Kth Largest Element in an Array"
excerpt: "Leetcode Kth Largest Element in an Array Java 풀이"
last_modified_at: 2021-10-20T13:00:00
header:
  image: /assets/images/leetcode/kth-largest-element-in-an-array.png
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
[Link](https://leetcode.com/problems/kth-largest-element-in-an-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int findKthLargest(int[] nums, int k) {
    Queue<Integer> queue = new PriorityQueue<>();
    for (int num : nums) {
      queue.add(num);
      if (queue.size() > k) {
        queue.poll();
      }
    }
    return queue.poll();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/574144798/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums의 k번째 큰 숫자를 찾아 반환하는 문제이다.

2. 숫자를 순위를 지정하여 저장하고 활용하기 위해서 [PriorityQueue](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html){:target="_blank"}를 정의한다.
- PriorityQueue는 기본적으로 낮은 숫자가 우선적으로 정렬되어 관리과 되며, 기존 Queue의 [FILO](https://en.wikipedia.org/wiki/FIFO_and_LIFO_accounting#LIFO){:target="_blank"}방식이 아니다.
  - 예를 들어, 아래와 같이 3 -> 1 순으로 넣으면 1 -> 3 순으로 나오게 된다.
  ```java
  Queue<Integer> queue = new PriorityQueue<>();
  queue.add(3);
  queue.add(1);
  System.out.println(queue.poll()); // 1
  System.out.println(queue.poll()); // 3
  ```
  - 하지만, 반대의 순서도 가능하다.
  ```java
  Queue<Integer> queue = new PriorityQueue<>(Collections.reverseOrder());
  queue.add(3);
  queue.add(1);
  System.out.println(queue.poll()); // 3
  System.out.println(queue.poll()); // 1
  ```
- 위의 PriorityQueue의 특성으로 Queue의 크기를 k까지 관리하면, k번째로 큰 값은 Queue의 가장 앞에 저장이 되게 된다.

3. 주어진 배열인 nums의 값들을 반복하여 Queue에 값들을 넣어 크기를 관리한다.
- queue에 nums에 속한 숫자인 num을 넣어준다.
- queue의 크기가 k보다 크게 되면, queue.poll()을 통해서 Queue 내의 가장 작은 값을 빼고 반복을 계속 수행한다.

4. 반복이 완료되면 주어진 배열인 nums의 가장 큰 k번째 값까지 저장된 queue에서 가장 작은 숫자인 k번째 큰 값을 빼서 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KthLargestElementInAnArray.java){:target="_blank"}에서 확인 가능합니다.