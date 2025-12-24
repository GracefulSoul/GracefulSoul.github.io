---
title: "Leetcode Java Apple Redistribution into Boxes"
excerpt: "Leetcode - 'Apple Redistribution into Boxes' 문제 Java 풀이"
last_modified_at: 2025-12-24T11:40:00
header:
  image: /assets/images/leetcode/apple-redistribution-into-boxes.png
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
[Link](https://leetcode.com/problems/apple-redistribution-into-boxes/){:target="_blank"}

# 코드
```java
class Solution {

  public int minimumBoxes(int[] apple, int[] capacity) {
    int sum = 0;
    for (int count : apple) {
      sum += count;
    }
    int result = 0;
    Arrays.sort(capacity);
    for (int i = capacity.length - 1; 0 <= i && 0 < sum; i--) {
      result++;
      sum -= capacity[i];
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/apple-redistribution-into-boxes/submissions/1863776323/){:target="_blank"}

# 설명
1. 각 사과 갯수가 저장된 apple로 각 사과를 담을 수 있는 크기가 저장된 박스가 저장된 capacity에 넣을 최소 박스의 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 apple에 저장된 모든 사과의 갯수를 저장할 변수로, apple 내 모든 값을 더해 넣어준다.
- result는 필요한 박스의 최소 갯수를 저장할 변수로, 0으로 초기화한다.

3. capacity를 오름차순 정렬 후, i를 capacity 마지막 위치부터 0 이하까지 i를 감소시키고 sum이 0 초과일 때 까지 아래를 반복한다.
- result인 사용한 박수 갯수를 증가시킨다.
- sum에 capacity[i]의 값인 박스에 넣은 사과의 갯수를 차감시켜준다.

4. 반복이 완료되면 사용된 박스의 갯수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AppleRedistributionIntoBoxes.java){:target="_blank"}에서 확인 가능합니다.