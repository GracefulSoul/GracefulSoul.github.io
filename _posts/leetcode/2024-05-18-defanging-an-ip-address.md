---
title: "Leetcode Java Defanging an IP Address"
excerpt: "Leetcode Easy - 'Defanging an IP Address' 문제 Java 풀이"
last_modified_at: 2024-05-18T10:30:00
header:
  image: /assets/images/leetcode/defanging-an-ip-address.png
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
[Link](https://leetcode.com/problems/defanging-an-ip-address/){:target="_blank"}

# 코드
```java
class Solution {

  public String defangIPaddr(String address) {
    StringBuilder sb = new StringBuilder();
    for (char c : address.toCharArray()) {
      sb.append(c == '.' ? "[.]" : c);
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/defanging-an-ip-address/submissions/1260937901/){:target="_blank"}

# 설명
1. IPv4 프로토콜을 만족하는 address 내 마침표(".")를 "[.]" 문자열로 변환하는 문제이다.

2. sb는 동적으로 조건에 만족하는 문자열을 만들 변수로, address의 모든 문자들을 순차적으로 반복하여 마침표 문자의 경우만 "[.]" 문자열로 바꿔 문자열로 변환 후 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DefangingAnIPAddress.java){:target="_blank"}에서 확인 가능합니다.