---
title: "Leetcode Java Random Pick with Weight"
excerpt: "Leetcode - 'Random Pick with Weight' 문제 Java 풀이"
last_modified_at: 2022-06-13T19:30:00
header:
  image: /assets/images/leetcode/random-pick-with-weight.png
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
[Link](https://leetcode.com/problems/random-pick-with-weight/){:target="_blank"}

# 코드
```java
class Solution {

  private Random random;
  private int[] sum;
  private int length;

  public Solution(int[] w) {
    this.random = new Random();
    for (int i = 1; i < w.length; ++i) {
      w[i] += w[i - 1];
    }
    this.sum = w;
    this.length = w.length;
  }

  public int pickIndex() {
    int left = 0;
    int right = this.length - 1;
    int index = this.random.nextInt(this.sum[this.length - 1]) + 1;
    while (left < right) {
      int mid = left + (right - left) / 2;
      if (this.sum[mid] == index) {
        return mid;
      } else if (this.sum[mid] < index) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }
    return left;
  }

}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(w);
 * int param_1 = obj.pickIndex();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/721150148/){:target="_blank"}

# 설명
1. w 내 값을 저장하고 임의 확률대로 반환하는 Solution 객체를 완성하는 문제이다.
- 생성자인 Solution(int[] w)은 w를 이용하여 객체를 초기화한다.
- 메서드인 pickIndex()는 아래의 확률대로 w 내 임의 값을 반환하는 역할을 수행한다.
  - w 내 모든 값의 합을 sum이라 할 때, w[i]의 선택 확률은 $\frac{w[i]}{sum}$

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- random은 임의 확률로 값을 반환하기 위한 변수이다.
- sum은 생성자를 통해 주입된 w의 각 요소 별 누계를 넣어 저장할 배열이다.
- length는 생성자를 통해 주입된 w의 길이를 저장할 변수이다.

3. 생성자인 Solution(int[] w)을 완성한다.
- random에 java의 Random 객체로 초기화한다.
- w를 반복하여 이전 값을 누계한 후 sum에 넣어준다.
- length에 w의 길이를 넣어 초기화한다.

4. 메서드인 pickIndex()를 완성한다.
- left에 0, right에 $length - 1$을 넣어 초기화한다.
- index에 random을 활용하여 0부터 sum의 가장 큰 값 사이의 임의 값을 가져와 1을 더한 값을 넣어준다.
- left가 right 미만일 때 까지 반복하여 아래를 수행하여 탐색을 수행한다.
  - mid에 $left + \frac{right - left}{2}$를 넣어준다.
  - sum의 mid번째 값이 index인 경우, mid를 반환한다.
  - sum의 mid번째 값이 index보다 작은 경우, left에 $mid + 1$을 넣어 값의 범위를 좁혀준다.
  - sum의 mid번째 값이 index보다 큰 경우, right에 mid를 넣어 값의 범위를 좁혀준다.
- 반복이 완료되면 index 값에 가까운 값이 계산된 위치인 left를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/object/solution/random/pick/weight/Solution.java){:target="_blank"}에서 확인 가능합니다.