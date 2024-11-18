---
title: "Leetcode Java Defuse the Bomb"
excerpt: "Leetcode - 'Defuse the Bomb' 문제 Java 풀이"
last_modified_at: 2024-11-18T18:40:00
header:
  image: /assets/images/leetcode/defuse-the-bomb.png
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
[Link](https://leetcode.com/problems/defuse-the-bomb/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] decrypt(int[] code, int k) {
    if (k == 0) {
      return new int[code.length];
    }
    int length = code.length;
    int start = 1;
    int end = k;
    if (k < 0) {
      start = length + k;
      end = length - 1;
    }
    int sum = 0;
    for (int i = start; i <= end; i++) {
      sum += code[i];
    }
    int[] result = new int[length];
    for (int i = 0; i < length; i++) {
      result[i] = sum;
      sum -= code[start++ % length] - code[++end % length];
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/defuse-the-bomb/submissions/1456085350/){:target="_blank"}

# 설명
1. code에서 아래의 규칙대로 합계를 각 위치에서 계산하여 반환하는 문제이다.
- k가 0보다 큰 경우, 현재 값의 위치에서 다음 k개 숫자의 합을 넣는다.
- k가 0보다 작은 경우, 현재 값의 위치에서 이전 k개 숫자의 합을 넣는다. (여기서 k는 절댓값 k이다.)
- k가 0인 경우, 모든 위치의 값은 0이다.

2. k가 0인 경우, code 길이의 정수 배열을 정의하여 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- length는 code의 길이를 저장한 변수이다.
- start와 end는 시작 위치와 종료 위치를 저장할 변수로, 아래의 경우에 따라 값을 넣어준다.
  - k가 0보다 큰 경우, start에 1과 end에 k를 넣어준다.
  - k가 0보다 작은 경우, start에 $length + k$와 end에 $length - 1$을 넣어준다.
- sum은 위치에 따라 k개 값의 합을 저장할 변수로, start부터 end까지 code 내 값의 합을 넣어준다.
- result는 결과를 저장할 변수로, length 크기의 정수 배열로 초기화한다.

4. 0부터 length 미만까지 i를 증가시키면서 아래를 수행한다.
- result[i]의 위치에 사전 계산된 sum을 먼저 넣어준다.
- sum에 code에서 start를 length로 나눈 나머지 값의 위치에 해당하는 값을 뺀 후 start를 증가시키고, end를 증가시킨 후 length 나눈 나머지 값의 위치에 해당하는 값을 더해준다.

5. 반복이 완료되면 각 위치별 조건에 해당하는 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DefuseTheBomb.java){:target="_blank"}에서 확인 가능합니다.