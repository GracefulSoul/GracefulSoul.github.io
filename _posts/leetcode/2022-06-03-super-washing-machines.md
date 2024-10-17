---
title: "Leetcode Java Super Washing Machines"
excerpt: "Leetcode - 'Super Washing Machines' 문제 Java 풀이"
last_modified_at: 2022-06-03T06:00:00
header:
  image: /assets/images/leetcode/super-washing-machines.png
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
[Link](https://leetcode.com/problems/super-washing-machines/){:target="_blank"}

# 코드
```java
class Solution {

  public int findMinMoves(int[] machines) {
    int total = 0;
    int length = machines.length;
    for (int machine : machines) {
      total += machine;
    }
    if (total % length != 0) {
      return -1;
    }
    int avg = total / length;
    int count = 0;
    int max = 0;
    int diff = 0;
    for (int machine : machines) {
      diff = machine - avg;
      count += diff;
      max = Math.max(Math.max(max, Math.abs(count)), diff);
    }
    return max;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/711659468/){:target="_blank"}

# 설명
1. 세탁기 내 옷의 개수를 담은 machines 배열의 모든 값들을 동일하게 맞추기 위한 최소 횟수를 구하는 문제이다.
- 단, 동일하게 맞추지 못하는 경우 -1을 주어진 문제의 결과로 반환한다.

2. 사전 검증에 필요한 변수를 정의한다.
- total은 모든 세탁기 내 옷의 개수를 저장할 변수로, machines를 반복하여 모든 옷의 개수를 더해준다.
- length는 machines의 길이를 저장한 변수이다.

3. total을 length로 나눈 나머지 값이 0이 아닌 경우 모든 세탁기에 옷을 동일한 개수로 분배할 수 없으므로, -1을 주어진 문제의 결과로 반환한다.

4. 문제 풀이에 필요한 변수를 정의한다.
- avg는 각 세탁기에 옷을 나눠 넣을 개수를 저장할 변수로, total을 length로 나눈 결과를 저장한다.
- count는 세탁기에 옷을 고르게 넣을 때 필요한 옷의 개수를 저장할 변수로, 0으로 초기화한다.
- max는 세탁기 내 옷의 개수를 동일하게 맞추기 위한 최소 이동 횟수를 저장하기 위한 변수로, 0으로 초기화한다.
- diff는 세탁기의 부족한 옷의 개수를 저장하기 위한 변수로, 0으로 초기화한다.

5. machines의 모든 값을 반복하여 아래를 수행한다.
- diff에 machine에 avg를 뺀 값인 현재 세탁기의 부족하거나 여유있는 옷의 개수를 넣어준다.
- count에는 diff를 추가하여 현재까지 고르게 분배하기 위한 부족하거나 여유있는 옷의 개수를 저장한다.
- max, count의 절댓값, diff 세 값 중 가장 큰 값을 max에 넣어준다.
  - count의 절댓값은 부족하거나(-) 여유있는(+) 옷을 이동하는 횟수로 부호가 중요하지 않고 값이 중요하기 때문에 절댓값으로 변환하여 비교를 한다.

6. 반복이 완료되면 최소 횟수를 저장한 max를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SuperWashingMachines.java){:target="_blank"}에서 확인 가능합니다.