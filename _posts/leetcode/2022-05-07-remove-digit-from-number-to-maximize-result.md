---
title: "Leetcode Java Remove Digit From Number to Maximize Result"
excerpt: "Leetcode - 'Remove Digit From Number to Maximize Result' 문제 Java 풀이"
last_modified_at: 2022-05-07T18:00:00
header:
  image: /assets/images/leetcode/remove-digit-from-number-to-maximize-result.png
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
[Link](https://leetcode.com/problems/remove-digit-from-number-to-maximize-result/){:target="_blank"}

# 코드
```java
class Solution {

  public String removeDigit(String number, char digit) {
    char[] nums = number.toCharArray();
    int index = 0;
    for (int idx = 0; idx < number.length(); idx++) {
      if (nums[idx] == digit) {
        index = idx;
        if (idx < number.length() - 1 && nums[idx] < nums[idx + 1]) {
          break;
        }
      }
    }
    return number.substring(0, index).concat(number.substring(index + 1));
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/694661722/){:target="_blank"}

# 설명
1. 숫자로 이루어진 문자열 number 내 digit인 문자가 최소 한 번 이상 들어가 있는데, 해당 digit을 제거한 결과가 가장 큰 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- nums는 number를 문자 배열로 변환해서 저장하는 변수이다.
- index는 제거할 문자의 위치를 저장할 변수로, 0으로 초기화한다.

3. 0부터 number의 길이 미만까지 idx를 증가시키며 아래를 수행한다.
- nums의 idx번 문자가 digit인 경우, index에 idx를 넣어준다.
- idx가 number의 마지막 문자가 아니고 다음 위치의 값인 $idx + 1$번째 값이 더 큰 경우, 해당 문자를 제거해야 하므로 반복을 중단한다.

4. 반복이 완료되어 제거할 문자의 위치를 탐색하였으면, number를 해당 문자 이전과 이후로 분리해서 하나의 문자열로 만들어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveDigitFromNumberToMaximizeResult.java){:target="_blank"}에서 확인 가능합니다.