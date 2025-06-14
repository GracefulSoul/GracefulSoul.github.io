---
title: "Leetcode Java Maximum Difference by Remapping a Digit"
excerpt: "Leetcode - 'Maximum Difference by Remapping a Digit' 문제 Java 풀이"
last_modified_at: 2025-06-14T16:00:00
header:
  image: /assets/images/leetcode/maximum-difference-by-remapping-a-digit.png
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
[Link](https://leetcode.com/problems/maximum-difference-by-remapping-a-digit/){:target="_blank"}

# 코드
```java
class Solution {

  public int minMaxDifference(int num) {
    String str = String.valueOf(num);
    char[] max = str.toCharArray();
    char[] min = str.toCharArray();
    char replace = ' ';
    for (char c : max) {
      if (c != '9') {
        replace = c;
        break;
      }
    }
    for (int i = 0; i < max.length; i++) {
      if (max[i] == replace) {
        max[i] = '9';
      }
    }
    replace = min[0];
    for (int i = 0; i < min.length; i++) {
      if (min[i] == replace) {
        min[i] = '0';
      }
    }
    return Integer.parseInt(String.valueOf(max)) - Integer.parseInt(String.valueOf(min));
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-difference-by-remapping-a-digit/submissions/1663575192/){:target="_blank"}

# 설명
1. num의 숫자들 중 하나의 숫자를 선택하여 [0, 9]로 바꾸었을 때 최댓값과 최솟값을 구한 후, 두 값의 차잇값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- str은 num을 문자열로 변환한 변수이다.
- max와 min은 최댓값과 최솟값으 문자를 변환하여 저장할 변수로, str의 문자 배열로 초기화한다.
- replace는 변환할 문자열을 저장할 변수로, 임의 문자열인 ' '로 초기화하고 max의 문자를 순차적으로 c에 넣은 후 순차적으로 c가 9가 아니면 replace에 c를 넣어준다.

3. 0부터 max의 길이 미만까지 i를 증가시키며, max[i]의 값이 replace와 같은 문자열을 모두 '9'로 바꿔 최댓값 문자 배열로 변환한다.

4. replace를 min[0]의 첫 값으로 초기화 후 0부터 min의 길이 미만까지 i를 증가시키며 아래를 min[i]의 값이 replace와 동일한 경우, min[i]에 '0'을 넣어 최솟값 문자여롤 변환한다.

5. max와 min을 정수형으로 변환 후 두 값의 차이를 주어진 문제의 결과로 반환한다.

# 해설
- 임의 값 num의 첫 번째 값과 동일한 값을 9로 바꿔주는 경우, 한 숫자만 바꿀 때 가장 큰 값이된다.
  - 예를 들어, 121212 -> 929292
- 임의 값 num의 첫 번째 값과 동일한 값을 0으로 바꿔주는 경우, 한 숫자만 바꿀 때 가장 작은 값이된다.
  - 예를 들어, 121212 -> 20202

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumDifferenceByRemappingADigit.java){:target="_blank"}에서 확인 가능합니다.