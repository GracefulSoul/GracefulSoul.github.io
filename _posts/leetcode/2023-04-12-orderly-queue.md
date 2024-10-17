---
title: "Leetcode Java Orderly Queue"
excerpt: "Leetcode - 'Orderly Queue' 문제 Java 풀이"
last_modified_at: 2023-04-12T20:55:00
header:
  image: /assets/images/leetcode/orderly-queue.png
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
[Link](https://leetcode.com/problems/orderly-queue){:target="_blank"}

# 코드
```java
class Solution {

  public String orderlyQueue(String s, int k) {
    if (k > 1) {
      char[] charArray = s.toCharArray();
      Arrays.sort(charArray);
      return new String(charArray);
    } else {
      String result = s;
      for (int i = 1; i < s.length(); i++) {
        String temp = s.substring(i) + s.substring(0, i);
        if (result.compareTo(temp) > 0) {
          result = temp;
        }
      }
      return result;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/orderly-queue/submissions/932461441/){:target="_blank"}

# 설명
1. s의 처음 k개의 문자 중 하나를 선택하여 문자열 끝에 추가할 때, 사전적인 순서가 낮은 문자열을 탐색하는 문제이다.

2. k가 1보다 큰 경우 문자열의 모든 문자는 차례대로 정렬이 가능하므로, s를 문자 배열로 번환하여 오름차순 정렬한 결과를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

3. k가 1인 경우, 아래를 수행한다.
- result에 s를 넣어주고, 1부터 s의 길이 미만까지 i를 증가시키며 아래를 반복한다.
  - temp에 s의 i번째 이후의 문자와 처음부터 i번째 미만까지 문자를 합친 결과를 넣어준다.
  - result와 비교하여 사전적 순서가 낮은 문자열을 result에 넣어준다.
- 반복이 완료되어 사전적 순서가 낮은 문자열이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/OrderlyQueue.java){:target="_blank"}에서 확인 가능합니다.