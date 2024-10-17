---
title: "Leetcode Java Restore IP Addresses"
excerpt: "Leetcode - 'Restore IP Addresses' 문제 Java 풀이"
last_modified_at: 2021-07-13T13:00:00
header:
  image: /assets/images/leetcode/restore-ip-addresses.png
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
[Link](https://leetcode.com/problems/restore-ip-addresses/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> restoreIpAddresses(String s) {
    List<String> ipAddresses = new ArrayList<>();
    this.recursive(s, ipAddresses, new StringBuilder(), 0, 0);
    return ipAddresses;
  }

  private void recursive(String s, List<String> list, StringBuilder sb, int index, int part) {
    if (index > s.length() || part > 4) {
      return;
    } else if (index == s.length() && part == 4) {
      list.add(sb.toString());
      return;
    } else {
      for (int length = 1; length <= 3; length++) {
        if (index + length > s.length()) {
          break;
        }
        int num = Integer.valueOf(s.substring(index, index + length));
        if (length == 1 || (length == 2 && num >= 10 && num <= 99) || (length == 3 && num >= 100 && num <= 255)) {
          sb.append(num);
          if (part < 3) {
            sb.append(".");
          }
          this.recursive(s, list, sb, index + length, part + 1);
          if (part < 3) {
            sb.deleteCharAt(sb.length() - 1);
          }
          sb.delete(sb.length() - length, sb.length());
        }
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/521632318/){:target="_blank"}

# 설명
1. 주어진 문자열 s를 이용하여 만들 수 있는 IP 주소를 모두 만드는 문제이다.

2. 재귀 호출을 이용하여 주어진 문자열 s를 이용한 IP를 StringBuilder를 통해 만들어 ipAddresses에 넣어준다.
- 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.

3. 문자열 s의 위치값인 index가 주어진 문자열 s의 길이보다 크거나 IP 주소의 구성의 4번째 파트(xxx.xxx.xxx.xxx)를 초과할 경우, 주어진 문자열로 IP 구성이 불가능하므로 반환시킨다.

4. 문자열 s의 위치값인 index가 주어진 문자열 s의 길이와 같고 IP 주소의 구성이 되었을 경우, list에 동적 문자열 조합을 하는 sb를 list에 추가하고 반환시킨다.

5. 3번과 4번의 경우가 아니면 최대 3문자까지 반복하여 IP 파트 구성을 한다.
- index와 IP 구성하려는 length의 합이 s의 길이보다 크다면 반복을 종료한다.
- part번째 파트를 구성하는 숫자를 검증하기 위해 num을 주어진 문자열 s의 index번째부터 $index + length$ 전까지 잘라 숫자로 변경하여 정의한다.
- length가 1자리거나, length가 2자리이며 num이 10 ~ 99이거나, length가 3자리이며 num이 100 ~ 255일 경우 아래의 내용을 수행한다.
  - 우선 sb에 num을 이어 넣어주고 part가 3 미만일 경우, IP 주소의 구성을 위해 "."을 이어 넣어준다.
  - index에 $index + length$, part에 $part + 1$을 넣어 재귀 호출을 수행한다.
  - 다시 part가 3 미만일 경우, 반복 수행을 위해 sb의 마지막 한 자리를 삭제해준다.
  - 주어진 s에서 사용한 문자열인 $sb.length() - length$부터 sb.length()까지의 길이만큼 sb에서 삭제해준다.
- 위의 반복을 계속 수행하여 만들 수 있는 IP 주소를 모두 만들어 준다.

6. 재귀 회출이 완료되면 ipAddresses를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RestoreIPAddresses.java){:target="_blank"}에서 확인 가능합니다.