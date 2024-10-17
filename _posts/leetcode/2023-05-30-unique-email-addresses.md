---
title: "Leetcode Java Unique Email Addresses"
excerpt: "Leetcode - 'Unique Email Addresses' 문제 Java 풀이"
last_modified_at: 2023-05-30T20:25:00
header:
  image: /assets/images/leetcode/unique-email-addresses.png
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
[Link](https://leetcode.com/problems/unique-email-addresses){:target="_blank"}

# 코드
```java
class Solution {

  public int numUniqueEmails(String[] emails) {
    Set<String> set = new HashSet<>();
    for (String email : emails) {
      int length = email.length();
      StringBuilder sb = new StringBuilder(length);
      for (int i = 0; i < length; i++) {
        char c = email.charAt(i);
        switch (c) {
          case '.':
            break;
          case '+':
            while (c != '@') {
              c = email.charAt(++i);
            }
            sb.append(email.substring(i));
            i = length;
            break;
          case '@':
            sb.append(email.substring(i));
            i = length;
            break;
          default:
            sb.append(c);
        }
      }
      set.add(sb.toString());
    }
    return set.size();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/unique-email-addresses/submissions/960198427/){:target="_blank"}

# 설명
1. 이메일 정보가 담긴 emails은 아래의 규칙을 만족한 고유한 이메일로 발송이 되는데, 발송되는 이메일의 수를 구하는 문제이다.
- emails[i]는 local명과 domain명을 '@'로 구분한 값을 담고 있다.
- local명에서는 '.' 문자는 무시하고 '+' 문자 이후는 제거한 local명으로 변환한 문자열로 변환하여 발송된다.

2. set은 고유한 이메일의 수를 저장할 변수로, 중복을 배제하기 위해서 HashSet으로 초기화한다.

3. emails를 차례대로 email에 넣고 아래를 반복한다.
- 조건을 만족하는 이메일로 변환하기 위한 변수를 정의한다.
  - length는 email의 길이를 저장한 변수이다.
  - sb는 동적으로 변환한 이메일을 저장할 변수로, email 크기의 StringBuilder로 초기화한다.
- 0부터 length까지 i를 증가시키며 아래를 반복한다.
  - c의 email의 i번째 문자를 넣어준다.
  - c가 '.'인 경우, 무시하고 다음 반복을 수행한다.
  - c가 '+'인 경우, 해당 문자부터 '@' 이전까지 문자들을 무시하고 모든 문자들을 sb에 넣어 set에 완성된 이메일을 넣고 i에 length를 넣어 다음 반복을 중단시킨다.
  - c가 '@'인 경우, sb에 남은 문자열을 넣고 i에 length를 넣어 다음 반복을 중단시킨다.
  - 위의 경우가 아니라면 sb에 c를 넣어준다.
- 반복이 완료되면 set에 완성된 이메일인 sb를 문자열을 변환하여 넣어준다.

4. 반복이 완료되면 고유 이메일의 수가 저장된 set의 크기를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UniqueEmailAddresses.java){:target="_blank"}에서 확인 가능합니다.