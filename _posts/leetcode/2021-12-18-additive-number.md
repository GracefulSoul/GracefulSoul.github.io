---
title: "Leetcode Java Additive Number"
excerpt: "Leetcode Additive Number Java 풀이"
last_modified_at: 2021-12-18T13:00:00
header:
  image: /assets/images/leetcode/additive-number.png
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
[Link](https://leetcode.com/problems/additive-number/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isAdditiveNumber(String num) {
    return this.recursive(num, -1, -1, 0, 0);
  }

  private boolean recursive(String num, long pre, long cur, int idx, int cnt) {
    int length = num.length();
    if (idx == length) {
      if (cur != -1 && pre != -1 && cnt > 2) {
        return true;
      } else {
        return false;
      }
    }
    long n = 0;
    for (int i = idx; i < length; i++) {
      n = n * 10 + (num.charAt(i) - '0');
      if (cur != -1 && pre != -1) {
        if (n == cur + pre) {
          if (this.recursive(num, cur, n, i + 1, cnt + 1)) {
            return true;
          }
        } else if (n > cur + pre) {
          return false;
        }
      }
      if (pre == -1) {
        if (this.recursive(num, n, cur, i + 1, cnt + 1)) {
          return true;
        }
      } else if (cur == -1) {
        if (this.recursive(num, pre, n, i + 1, cnt + 1)) {
          return true;
        }
      }
      if (n == 0) {
        break;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/603377076/){:target="_blank"}

# 설명
1. 숫자로 이루어진 주어진 문자열 num을 이용하여 숫자를 나눌 때, 이전 값과 현재 값의 합이 다음 값이 되는 조합으로 이루어져 있는지 검증하는 문제이다.

2. 문제 풀이에 사용할 재귀 호출 메서드인 recursive를 정의한다.
- 이전 값을 pre, 현재 값을 cur, 문자열의 위치 값인 idx, 숫자열의 개수를 저장할 cnt 변수로 활용한다.

3. length에 num의 길이를 저장한다.

4. idx가 length와 동일한 경우, 아래를 검증한다.
- cur과 pre가 -1이 아니고 cnt가 2보다 큰 경우 최소한 세 개 이상의 숫자열이 이전 값과 현재 값의 합이 다음 값이 되므로, true를 반환한다.
- 그렇지 않은 경우 문제를 충족하지 않으므로, false를 반환한다.

5. 값을 측정할 변수 n을 정의하고, idx부터 length까지 반복을 수행한다.
- n에 $n \times 10$에 num의 i번째 문자열의 숫자 값을 더해준다.
- cur과 pre가 -1인 경우, 아래를 검증한다.
  - n의 값이 $cur + pre$의 값과 동일한 경우, pre 자리에 cur을, cur 값에 n을, i 값에 $i + 1$을, cnt 값에 $cnt + 1$을 넣어 재귀 호출을 수행한 결과가 true인 경우 true를 반환한다.
  - n의 값이 $cur + pre$의 값보다 큰 경우, false를 반환한다.
- pre가 -1인 경우, 첫 검증을 수행하므로 아래를 수행한다.
  - pre 자리에 n을, cur 값에 cur을, i 값에 $i + 1$을, cnt 값에 $cnt + 1$을 넣어 재귀 호출을 수행한 결과가 true인 경우, true를 반환한다.
- pre가 -1이 아니고 cur이 -1인 경우, 아래를 수행한다.
  - pre 자리에 pre를, cur 값에 n을, i 값에 $i + 1$을, cnt 값에 $cnt + 1$을 넣어 재귀 호출을 수행한 결과가 true인 경우, true를 반환한다.
- n이 0인 경우 유효하지 않는 값이므로, 반복을 멈추고 false를 반환한다.
  - Note에 추가로 설명한 1, 02, 3 혹은 1, 2, 03 같이 0이 붙는 경우 유효하지 않는 값으로 판단한다.

6. 위에서 정의한 재귀 호출 메서드인 recursive를 pre와 cur에 -1을, idx와 cnt에 0을 넣어 num을 검증한 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AdditiveNumber.java){:target="_blank"}에서 확인 가능합니다.