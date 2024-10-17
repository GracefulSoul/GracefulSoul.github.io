---
title: "Leetcode Java Fruit Into Baskets"
excerpt: "Leetcode - 'Fruit Into Baskets' 문제 Java 풀이"
last_modified_at: 2023-04-19T19:20:00
header:
  image: /assets/images/leetcode/fruit-into-baskets.png
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
[Link](https://leetcode.com/problems/fruit-into-baskets){:target="_blank"}

# 코드
```java
class Solution {

  public int totalFruit(int[] fruits) {
    int length = fruits.length;
    int start = 0;
    int mid = 0;
    int max = 0;
    int[] baskets = new int[] { -1, -1 };
    for (int end = 0; end < length; end++) {
      int curr = fruits[end];
      if (curr != baskets[1]) {
        if (curr != baskets[0]) {
          max = Math.max(max, end - start);
          start = mid;
        }
        mid = end;
        baskets[0] = baskets[1];
        baskets[1] = curr;
      }
    }
    return Math.max(max, length - start);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/fruit-into-baskets/submissions/936292143/){:target="_blank"}

# 설명
1. 한 줄로 서있는 과일 나무의 과일 수를 담은 fruits를 이용하여 아래의 규칙대로 가장 많이 담은 과일의 수를 반환하는 문제이다.
- 제한 없이 담을 수 있는 두 바구니만 가지고 시작하여 한 바구니에는 같은 과일만 담을 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 fruits의 길이를 저장한 변수이다.
- start와 mid는 과일 나무의 시작 위치와 end 사이의 위치를 저장할 변수로, 둘 다 0으로 초기화한다.
- max는 최대와 과일의 수를 담을 변수로, 0으로 초기화한다.
- baskets는 제한 없이 담을 수 있는 두 바구니에 담긴 과일의 수를 넣을 변수로, 두 바구니에 담긴 과일의 수를 -1로 초기화한다.

3. 0부터 length 미만까지 마지막 과일 나무의 위치인 end를 증가시키며 아래를 수행한다.
- curr는 현재 과일의 갯수를 담을 변수로, fruits의 end번째 값을 넣어준다.
- curr이 baskets의 두 번째 값인 현재 바구니의 과일 수가 같지 않으면, 바구니의 과일 수를 갱신해야 하므로 아래를 수행한다.
  - curr이 baskets의 첫 번째 값인 이전 바구니의 과일 수가 같지 않으면, max에 max와 $end - start$ 중 큰 값을 넣고 start에 mid를 넣어준다.
  - mid에 end를 넣어 마지막 위치를 저장한다.
  - baskets의 첫 번째 위치에 두 번째 값을 넣고, baskets의 두번 째 값에 curr 값을 넣어 두 바구니의 과일 수를 갱신해준다.

4. 반복이 완료되면 max와 $length - start$ 중 큰 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FruitIntoBaskets.java){:target="_blank"}에서 확인 가능합니다.