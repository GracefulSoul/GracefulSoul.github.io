---
title: "Leetcode Java Remove K Digits"
excerpt: "Leetcode Remove K Digits Java 풀이"
last_modified_at: 2022-03-02T13:00:00
header:
  image: /assets/images/leetcode/remove-k-digits.png
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
[Link](https://leetcode.com/problems/remove-k-digits/){:target="_blank"}

# 코드
```java
class Solution {

  public String removeKdigits(String num, int k) {
    char[] numCharArray = num.toCharArray();
    int start = 0;
    int end = 0;
    for (int idx = 0; idx < numCharArray.length; idx++) {
      if (end > 0 && k > 0 && numCharArray[end - 1] > numCharArray[idx]) {
        k--;
        idx--;
        end--;
      } else {
        numCharArray[end++] = numCharArray[idx];
      }
    }
    if (k > 0) {
      end -= k;
    }
    while (end > start && numCharArray[start] == '0') {
      start++;
    }
    return start == end ? "0" : new String(numCharArray, start, end - start);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/651635861/){:target="_blank"}

# 설명
1. 숫자로 구성된 주어진 문자열 num 중 k개의 숫자를 제거하여 가장 작은 숫자를 문자열로 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- numCharArray는 num의 각 문자들을 활용하기 위한 배열로, num을 문자 배열로 변환하여 저장한다.
- start는 문자열로 변환하기 위한 시작 인덱스로, 0으로 초기화한다.
- end는 문자열로 변환하기 위한 종료 인덱스로, 0으로 초기화한다.

3. 0부터 numCharArray의 길이만큼 idx를 증가시키며 반복하여 순서대로 만들 수 있는 작은 값 순으로 정렬을 수행한다.
- end와 k가 0보다 크고 numCharArray의 $end - 1$번째 값이 idx번째 값보다 큰 경우, k와 idx와 end를 감소시킨다.
- 위의 경우가 아닌 경우, numCharArray의 end번째 자리에 idx번째 문자를 넣고 end를 증가시킨다.

4. k가 0보다 큰 경우 뒤의 k개는 무시해도 되는 큰 수이므로, end를 k만큼 빼준다.

5. end가 start보다 크고 numCharArray의 start번째 문자가 0인 경우, 숫자의 시작을 0이 아닌 숫자로 하기 위해 start를 계속 증가시킨다.

6. start가 end와 동일한 경우 문자열에서 포함된 숫자열이 없으므로 "0"을, 그렇지 않은 경우 numCharArray의 start부터 $end - start$까지 문자열로 변화하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveKDigits.java){:target="_blank"}에서 확인 가능합니다.