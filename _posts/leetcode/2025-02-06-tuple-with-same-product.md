---
title: "Leetcode Java Tuple with Same Product"
excerpt: "Leetcode - 'Tuple with Same Product' 문제 Java 풀이"
last_modified_at: 2025-02-06T19:00:00
header:
  image: /assets/images/leetcode/tuple-with-same-product.png
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
[Link](https://leetcode.com/problems/tuple-with-same-product/){:target="_blank"}

# 코드
```java
class Solution {

  public int tupleSameProduct(int[] nums) {
    int length = nums.length;
    Map<Integer, Integer> map = new HashMap<>();
    int result = 0;
    for (int i = 0; i < length; i++) {
      for (int j = i + 1; j < length; j++) {
        int key = nums[i] * nums[j];
        int value = map.getOrDefault(key, 0);
        result += 8 * value;
        map.put(key, value + 1);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/tuple-with-same-product/submissions/1533415899/){:target="_blank"}

# 설명
1. nums의 값들을 이용하여 $a \times b = c \times d$를 만족하는 각 값이 모두 다른 임의 네 값인 a, b, c, d의 조합의 갯수를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- map은 임의 두 값의 곱에 대한 갯수를 0-index로 계산하기 위한 변수로, key-value로 저장하기 위해 HashMap으로 초기화한다.

- result는 조합의 갯수를 저장하기 위한 변수로, 0으로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키고, $i + 1$부터 length 미만까지 j를 증가시키며 아래를 반복한다.
- key에 $nums[i] \ times[j]$인 두 값의 곱을 넣어준다.
- value에 map에서 key에 대한 값이 존재하면 꺼내 넣어주고, 없는 경우 0을 넣어준다.
- result에 $8 \times value$의 값인 조합의 수를 더해준다.
- map의 key에 해당 하는 값을 $value + 1$로 넣어 갯수를 증가시켜준다.

4. 반복이 완료되면 각 조합의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 해설
- 두 값의 곱이 동일한 값이 2개가 존재해야 하나의 조합이므로 0-index로 시작하고, 2개는 $2 \times 2 \times 2 \times 2 \times 2 = 8$ 개의 조합의 갯수가 존재한다.
  - nums = [1, 3, 4, 12]의 경우, 아래의 총 8개 조합이 존재한다.
  - [1, 12, 3, 4], [1, 12, 4, 3], [12, 1, 3, 4], [12, 1, 4, 3], [3, 4, 1, 12], [3, 4, 12, 1], [4, 3, 1, 12], [4, 3, 12, 1]
- 두 값의 곱이 동일한 값이 3개가 존재하면 이미 2개의 조합에 대한 값을 result에 더했으므로, 위의 공식에 따라 다른 한 값과 나머지 두 개의 조합의 경우인 $8 \time 2 = 16$ 개의 조합의 갯수가 존재한다.
- 위에 따라 두 값의 곱이 동일한 값을 0-index로 산출하고, 각 갯수에 따라 8개의 경우의 수를 곱한 값을 누계하면 모든 조합의 갯수가 완성된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TupleWithSameProduct.java){:target="_blank"}에서 확인 가능합니다.