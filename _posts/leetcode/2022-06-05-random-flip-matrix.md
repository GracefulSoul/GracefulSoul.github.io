---
title: "Leetcode Java Random Flip Matrix"
excerpt: "Leetcode Random Flip Matrix Java"
last_modified_at: 2022-06-05T09:00:00
header:
  image: /assets/images/leetcode/random-flip-matrix.png
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
[Link](https://leetcode.com/problems/random-flip-matrix/){:target="_blank"}

# 코드
```java
class Solution {

  private Map<Integer, Integer> map;
  private int m;
  private int n;
  private int total;
  private Random random;

  public Solution(int m, int n) {
    this.random = new Random();
    this.m = m;
    this.n = n;
    this.reset();
  }

  public int[] flip() {
    int num = this.random.nextInt(this.total--);
    int value = this.map.getOrDefault(num, num);
    this.map.put(num, this.map.getOrDefault(this.total, this.total));
    this.map.put(this.total, value);
    return new int[] { value / this.n, value % this.n };
  }

  public void reset() {
    this.map = new HashMap<>();
    this.total = this.m * this.n;
  }

}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(m, n);
 * int[] param_1 = obj.flip();
 * obj.reset();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/714531703/){:target="_blank"}

# 설명
1. $m \times n$ 크기의 이차원 배열은 모두 0으로 채워져 있으나, 특정 셀을 랜덤하게 선택하여 해당 행과 열을 배열로 반환하고 1로 뒤집는 Solution 클래스를 완성하는 문제이다.
- 생성자인 Solution(int m, int n)은 객체를 초기화하는 역할을 수행한다.
- 메서드인 flip()은 임의 셀을 선택하여 해당 값을 1로 변경 후, 해당 셀의 위치 값을 배열로 반환한다.
- 메서드인 reset()은 배열 내 값을 0으로 초기화하는 역할을 수행한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 [Fisher–Yates shuffle](https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle){:target="_blank"} 방식을 활용하여 임의 위치의 값을 저장하기 위한 변수이다.
- m은 2차원 배열의 행, n은 열을 나타내고, total은 $m \times n$의 크기르 저장하기 위한 변수이다.
- random은 임의 위치를 동일한 확률로 탐색하기 위한 변수이다.

3. 생성자인 Solution(int m, int n)을 정의한다.
- random에 Java의 Random 객체를 정의해 넣어준다.
- m과 n은 주어진 m과 n을 이용하여 값을 넣어주고, 5번에서 정의한 reset() 메서드를 호출하여 나머지 객체를 초기화한다.

4. 메서드인 flip()을 정의한다.
- num에 random을 활용하여 0 ~ total 까지의 임의 숫자인 인덱스를 생성하고 total을 감소시킨다.
- value에 map 내 num이 키인 값이 있는지 확인하여 가져와 넣어주고, 없을 경우 num을 넣어준다.
- map 내 total이 키인 값이 있으면 해당 값을, 없을 경우 total을 map 내 num이 키인 값에 넣어준다.
- value를 행인 n으로 나누어 값을 행으로, 나머지를 열로 배열을 만들어 반환한다.

5. 메서드인 reset()을 정의한다.
- map에 HashMap을 넣어 초기화한다.
- total에 2차원 배열의 크기인 $m \times n$을 넣어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/object/solution/random/flip/Solution.java){:target="_blank"}에서 확인 가능합니다.