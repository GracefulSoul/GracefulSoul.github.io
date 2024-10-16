---
title: "Leetcode Java Validate IP Address"
excerpt: "Leetcode Validate IP Address Java 풀이"
last_modified_at: 2022-04-26T12:00:00
header:
  image: /assets/images/leetcode/validate-ip-address.png
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
[Link](https://leetcode.com/problems/validate-ip-address/){:target="_blank"}

# 코드
```java
class Solution {

  public String validIPAddress(String queryIP) {
    if (this.isIPv4(queryIP)) {
      return "IPv4";
    } else if (this.isIPv6(queryIP)) {
      return "IPv6";
    } else {
      return "Neither";
    }
  }

  private boolean isIPv4(String queryIP) {
    String[] octets = queryIP.split("\\.", -1);
    if (octets.length != 4) {
      return false;
    }
    for (String octet : octets) {
      if (octet.length() == 0 || octet.length() > 3 || (octet.charAt(0) == '0' && octet.length() != 1)) {
        return false;
      }
      int num = 0;
      for (int c : octet.toCharArray()) {
        if (c >= '0' && c <= '9') {
          num = (num * 10) + (c - '0');
        } else {
          return false;
        }
      }
      if (num > 255) {
        return false;
      }
    }
    return true;
  }

  private boolean isIPv6(String queryIP) {
    String[] octets = queryIP.split(":", -1);
    if (octets.length != 8) {
      return false;
    }
    for (String octet : octets) {
      if (octet.length() > 4 || octet.length() == 0) {
        return false;
      }
      for (int c : octet.toCharArray()) {
        if (!((c >= '0' && c <= '9') || (c >= 'a' && c <= 'f') || (c >= 'A' && c <= 'F'))) {
          return false;
        }
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/687572415/){:target="_blank"}

# 설명
1. 문자열 queryIP가 유효한 IP인지를 검증하는 문제이다.
- IP는 "IPv4"와 "IPv6" 두 버전의 경우 해당 문자열을 반환하고, 그 외의 경우 "Neither" 문자열을 반환한다.

2. queryIP가 IPv4인지 검증하기 위한 isIPv4(String queryIP) 메서드를 정의한다.
- queryIP를 마침표(".") 기준으로 분리해서 octets에 넣어준다.
- octets의 길이가 4가 아닌 경우 유효한 IPv4 구조가 아니므로, false를 반환한다.
- octets의 모든 값들을 아래를 통해 검증한다.
  - octet의 길이가 0이거나 3을 초과하거나 첫 값이 0으로 시작하지만 한 글자가 아닌 경우 IPv4의 유효한 octet이 아니므로, false를 반환한다.
  - num을 0으로 정의하여 octet의 모든 값들을 정수로 치환한 값을 넣어주고, 정수가 아닌 값이 존재하면 false를 반환한다.
  - num이 255를 초과하는 경우도 유효한 IPv4 구조가 아니므로, false를 반환한다.
- 반복이 완료되면 queryIP가 유효한 IPv4이므로, true를 반환한다.

3. queryIP가 IPv6인지 검증하기 위한 isIPv6(String queryIP) 메서드를 정의한다.
- queryIP를 콜론(":") 기준으로 분리해서 octets에 넣어준다.
- octets의 길이가 8이 아닌 경우 유효한 IPv6 구조가 아니므로, false를 반환한다.
  - octets의 모든 값을 아래를 통해 검증한다.
  - octet의 길이가 0이거나 4초과인 경우 IPv6의 유효한 octet이 아니므로, false를 반환한다.
  - octet의 모든 문자들이 0 ~ 9, a ~ z, A ~ F외 문자가 들어가는 경우, IPv6의 유효한 octet이 아니므로 false를 반환한다.
- 반복이 완료되면 queryIP가 유효한 IPv6이므로, true를 반환한다.

4. 아래의 각 경우에 따라 문자열을 주어진 문제의 결과로 반환한다.
- 2번에서 정의한 isIPv4(String queryIP) 메서드의 수행 결과가 true이면, "IPv4"를 주어진 문제의 결과로 반환한다.
- 3번에서 정의한 isIPv6(String queryIP) 메서드의 수행 결과가 true이면, "IPv6"를 주어진 문제의 결과로 반환한다.
- 그 외의 경우 유효한 IP 구조가 아니므로, "Neither"를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidateIPAddress.java){:target="_blank"}에서 확인 가능합니다.