---
title: "Leetcode Java Check If N and Its Double Exist"
excerpt: "Leetcode - 'Check If N and Its Double Exist' 문제 Java 풀이"
last_modified_at: 2024-12-01T10:50:00
header:
  image: /assets/images/leetcode/check-if-n-and-its-double-exist.png
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
[Link](https://leetcode.com/problems/check-if-n-and-its-double-exist/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean checkIfExist(int[] arr) {
    Set<Integer> set = new HashSet<>();
    for (int num : arr) {
      if (set.contains(num * 2) || (num % 2 == 0 && set.contains(num / 2))) {
        return true;
      } else {
        set.add(num);
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/check-if-n-and-its-double-exist/submissions/1466894404/){:target="_blank"}

# 설명
1. arr 내 임의 값과 해당 값의 두 배가 되는 값이 존재하는지 찾는 문제이다.

2. set은 중복되지 않은 값을 저장하기 위한 변수로, HashSet으로 초기화한다.

3. arr의 값을 순차적으로 num에 넣어 아래를 수행한다.
- 아래의 경우 중 하나라도 만족하면 true를 주어진 문제의 결과로 반환한다.
  - set에 $num \times 2$의 값이 존재하는 경우.
  - num이 짝수이면서, set에 2로 나눈 값이 존재하는 경우.
- 위의 경우가 아니라면, set에 num을 더해준다.

4. 위의 반복이 완료되면 조건을 만족하는 값들이 존재하지 않으므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CheckIfNAndItsDoubleExist.java){:target="_blank"}에서 확인 가능합니다.