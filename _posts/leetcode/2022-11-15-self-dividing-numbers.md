---
title: "Leetcode Java Self Dividing Numbers"
excerpt: "Leetcode - 'Self Dividing Numbers' 문제 Java 풀이"
last_modified_at: 2022-11-15T18:55:00
header:
  image: /assets/images/leetcode/self-dividing-numbers.png
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
[Link](https://leetcode.com/problems/self-dividing-numbers){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> selfDividingNumbers(int left, int right) {
    List<Integer> result = new ArrayList<>();
    for (int idx = left; idx <= right; idx++) {
      int num = idx;
      boolean valid = true;
      while (num > 0) {
        int remain = num % 10;
        if (remain == 0 || idx % remain != 0) {
          valid = false;
          break;
        }
        num /= 10;
      }
      if (valid) {
        result.add(idx);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/843824546/){:target="_blank"}

# 설명
1. [left, right] 구간 내 각 자릿수에 해당하는 값들로 해당 숫자를 나누었을 때 나머지가 모두 0이 되는 자기 나눗셈 숫자를 구하는 문제이다.

2. 결과를 넣을 result를 ArrayList로 초기화한다.

3. left부터 right까지 idx를 증가시키며 아래를 반복한다.
- num에 idx를 넣어주고, 자기 나눗셈 숫자를 검증한 결과를 넣기 위한 valid를 true로 초기화한다.
- num이 0 초과일 때 까지 remain에 num을 10으로 나눈 나머지 값을 넣고 자기 나눗셈 숫자가 될 수 없으므로 valid를 false로 넣고 반복을 중지하고, 아니면 num에 10으로 나눈 값을 넣어 반복을 계속한다.
  - num을 10으로 나눈 나머지가 0인 경우 나눗셈을 진행할 수 없다.
  - idx를 remain으로 나눈 나머지가 0이 아닌 경우 만족하지 않는다.
- 위의 반복이 완료되고 valid가 true이면 idx는 자기 나눗셈 숫자이므로, result에 idx를 넣어준다.

4. 반복이 완료되면 [left, right] 구간 내 존재하는 자기 나눗셈 숫자를 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SelfDividingNumbers.java){:target="_blank"}에서 확인 가능합니다.