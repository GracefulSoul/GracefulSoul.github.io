---
title: "Leetcode Java Odd Even Jump"
excerpt: "Leetcode Hard - 'Odd Even Jump' 문제 Java 풀이"
last_modified_at: 2023-08-16T20:00:00
header:
  image: /assets/images/leetcode/odd-even-jump.png
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
[Link](https://leetcode.com/problems/odd-even-jump){:target="_blank"}

# 코드
```java
class Solution {

  public int oddEvenJumps(int[] arr) {
    int length = arr.length;
    boolean[] higher = new boolean[length];
    boolean[] lower = new boolean[length];
    higher[length - 1] = true;
    lower[length - 1] = true;
    TreeMap<Integer, Integer> map = new TreeMap<>();
    map.put(arr[length - 1], length - 1);
    for (int i = length - 2; i >= 0; i--) {
      Map.Entry<Integer, Integer> next = map.ceilingEntry(arr[i]);
      if (next != null) {
        higher[i] = lower[next.getValue()];
      }
      next = map.floorEntry(arr[i]);
      if (next != null) {
        lower[i] = higher[next.getValue()];
      }
      map.put(arr[i], i);
    }
    int result = 0;
    for (int i = 0; i < length; i++) {
      if (higher[i]) {
        result++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/odd-even-jump/submissions/1022891491/){:target="_blank"}

# 설명
1. arr의 임의 위치에서 아래를 만족하는 이동이 가능한 위치들의 갯수를 계산하는 문제이다.
- 이동은 홀수 혹은 짝수 점프를 이용한다.
- 홀수 점프는 arr[i] <= arr[j]를 만족할 때, arr[j]가 가장 작은 값이 되는 점프이다.
- 짝수 점프는 arr[i] >= arr[j]를 만족할 때, arr[j]가 가장 큰 값이 되는 점프이다.
- 두 점프 모두 여러 개의 j가 존재할 경우, 가장 작은 j로만 점프할 수 있다.
- 시작 위치부터 배열의 끝에 도달할 수 있는 경우만 계산한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 arr의 길이를 저장한 변수이다.
- higher는 점층적으로 증가하는 추세를 저장하기 위한 변수로, 변수의 최대 수인 length 크기인 부울 배열로 초기화하고 마지막 위치에 true를 넣어준다.
- lower는 점층적으로 증가하는 추세를 저장하기 위한 변수로, 변수의 최대 수인 length 크기인 부울 배열로 초기화한다 마지막 위치에 true를 넣어준다.
- map은 arr의 값과 위치를 트리 형태로 저장하기 위한 변수로, TreeMap으로 초기화하고 arr의 마지막 값과 위치를 쌍으로 넣어준다.

3. $length - 2$부터 0까지 i를 감소시키며 아래를 반복한다.
- map에서 arr[i]보다 크거나 같은 키가 존재하는 경우, higher[i]에 lower 내 찾은 값에 해당하는 위치의 부울 값을 꺼내 넣어준다.
- map에서 arr[i]보다 작거나 같은 키가 존재하는 경우, lower[i]에 higher 내 찾은 값에 해당하는 위치의 부울 값을 꺼내 넣어준다.
- map에 arr[i]와 i를 넣어 TreeMap에 현재 값을 저장한다.

4. 반복이 완료되면 위치의 갯수를 저장할 result에 higher 내 true인 조건을 만족하는 위치의 갯수를 계산하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/OddEvenJump.java){:target="_blank"}에서 확인 가능합니다.