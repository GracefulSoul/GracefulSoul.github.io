---
title: "Leetcode Java License Key Formatting"
excerpt: "Leetcode - 'License Key Formatting' 문제 Java 풀이"
last_modified_at: 2022-05-09T13:00:00
header:
  image: /assets/images/leetcode/license-key-formatting.png
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
[Link](https://leetcode.com/problems/license-key-formatting/){:target="_blank"}

# 코드
```java
class Solution {

  public String licenseKeyFormatting(String s, int k) {
    char[] chars = new char[s.length() * 2];
    int count = 0;
    int index = chars.length;
    for (int idx = s.length() - 1; idx >= 0; idx--) {
      char c = s.charAt(idx);
      if (c == '-') {
        continue;
      }
      if (count == k) {
        chars[--index] = '-';
        count = 0;
      }
      chars[--index] = Character.toUpperCase(c);
      count++;
    }
    return String.valueOf(chars, index, chars.length - index);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/695887383/){:target="_blank"}

# 설명
1. 문자열 s를 이용하여 k개 단위로 이어진 숫자와 영대문자로 구성된 문자열과 해당 문자열 사이에 구분 기호인 "-" 문자를 이용하여 라이센스 키를 만드는 문제이다.
- 정확히 k 배수로 이루어진 문장이 아닌 경우, 앞의 문자열은 k개 이하로 구성한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- chars는 라이센스 키를 만들기 위한 문자를 넣을 배열로, k가 1인 경우 s 길이의 2배보다 1 작은 값이 되기 때문에 s의 2배의 크기로 초기화 한다.
- count는 k개의 숫자로 묶기 위해 사용하는 변수로, 0으로 초기화한다.
- index는 s를 거꾸로 탐색하기 위한 위치값을 넣을 변수로, chars의 길이로 초기화한다.

3. k배수로 이루어진 경우가 아니면 앞에 남은 문자로 이어야 하므로, s의 마지막 문자부터 거꾸로 idx를 감소시키며 반복을 수행한다.
- c에 s의 idx번째 문자를 넣어준다.
- c가 문자열 사이 구분 기호인 "-"인 경우, 다음 반복을 수행한다.
- count가 k인 경우, chars에 구분 기호인 "-"를 넣고 count를 0으로 초기화시켜준다.
- index를 감소시키고 chars의 index번째 자리에 c를 대문자로 변환하여 넣어준다.
- 문자를 넣었으므로 count를 증가시키고 반복을 계속 수행한다.

4. chars의 index번째 문자부터 $chars.length - index$ 문자까지 문자열로 만들어서 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LicenseKeyFormatting.java){:target="_blank"}에서 확인 가능합니다.