---
title: "Leetcode Java Build an Array With Stack Operations"
excerpt: "Leetcode Build an Array With Stack Operations Java"
last_modified_at: 2023-11-03T19:10:00
header:
  image: /assets/images/leetcode/build-an-array-with-stack-operations.png
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
[Link](https://leetcode.com/problems/build-an-array-with-stack-operations){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> buildArray(int[] target, int n) {
    List<String> list = new ArrayList<>();
    int i = 0;
    int j = 0;
    while (i++ <= n && j < target.length) {
      list.add("Push");
      if (target[j] == i) {
        j++;
      } else {
        list.add("Pop");
      }
    }
    return list;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/build-an-array-with-stack-operations/submissions/1090511942/){:target="_blank"}

# 설명
1. [1, n] 범위 내 값들을 이용하여 아래의 규칙대로 순차적으로 증가하는 값이 저장된 정수 배열인 target과 동일한 배열인 stack을 만들 수 있는 연산 순서를 반환하는 문제이다.
- target을 만들기 위한 기본 연산은 아래와 같다.
  - "Push"는 stack의 뒤에 값을 넣어준다.
  - "Pop"은 stack의 뒤에 있는 값을 빼준다.
- [1, n] 범위 내 값들을 순서대로 사용하여 위의 연산만 수행 가능하다.
- 범위 내 값들만 순차적으로 사용하여 연산을 수행한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- list는 연산을 순차적으로 넣을 변수로, ArrayList로 초기화한다.
- i는 [1, n] 범위 내 위치 j는 target 내 위치를 저장할 변수로, 둘 다 0으로 초기화한다.

3. i가 n 이하이면서 j가 target의 길이 미만까지 아래를 반복하면서 i를 증가시켜준다.
- list에 "Push"를 넣고 값을 추가해준다.
- target[j]의 값과 i와 동일한 경우, j를 증가시키고 아니면 list에 "Pop"을 추가하여 값을 제거한 것을 표시해준다.

4. 반복이 완료되면 연산 순서가 저장된 list를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BuildAnArrayWithStackOperations.java){:target="_blank"}에서 확인 가능합니다.