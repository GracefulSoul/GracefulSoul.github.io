---
title: "Leetcode Java Reorder Data in Log Files"
excerpt: "Leetcode Medium - 'Reorder Data in Log Files' 문제 Java 풀이"
last_modified_at: 2023-06-27T20:00:00
header:
  image: /assets/images/leetcode/reorder-data-in-log-files.png
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
[Link](https://leetcode.com/problems/reorder-data-in-log-files){:target="_blank"}

# 코드
```java
class Solution {

  public String[] reorderLogFiles(String[] logs) {
    Arrays.sort(logs, (s1, s2) -> {
      int index1 = s1.indexOf(" ") + 1;
      int index2 = s2.indexOf(" ") + 1;
      boolean isLetter1 = Character.isLetter(s1.charAt(index1));
      boolean isLetter2 = Character.isLetter(s2.charAt(index2));
      if (isLetter1 && isLetter2) {
        int compare = s1.substring(index1).compareTo(s2.substring(index2));
        if (compare != 0) {
          return compare;
        } else {
          return s1.compareTo(s2);
        }
      } else if (isLetter1 && !isLetter2) {
        return -1;
      } else if (!isLetter1 && isLetter2) {
        return 1;
      } else {
        return 0;
      }
    });
    return logs;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/reorder-data-in-log-files/submissions/980759529/){:target="_blank"}

# 설명
1. 아래의 두 형식의 로그로 이루어진 logs를 아래에서 명시한 순서대로 정렬하여 반환하는 문제이다.
- 각 로그의 첫 단어는 식별자이다.
- 문자 로그는 영어 소문자로만 구성된 로그이다.
- 숫자 로그는 숫자로만 구성된 로그이다.
- 문자 로그는 모든 숫자 로그 앞에 위치한다.
- 문자 로그는 사전 순으로 정렬하고 내용이 동일한 경우, 식별자의 사전순으로 정렬한다.
- 숫자 로그는 기존 순서를 유지하여 차례대로 유지한다.

2. logs의 임의 두 값을 s1과 s2에 넣어 아래를 수행한 결과에 따라 정렬한다.
- index1과 index2는 s1과 s2의 식별자 이후 내용의 위치를 넣을 변수로, s1과 s2의 첫 띄어쓰기(" ") 다음 위치로 넣어준다.
- isLetter1과 isLetter2는 s1과 s2가 문자 로그인지 검증하기 위한 변수로, s1과 s2의 내용 시작 단어가 문자인지를 검증한 결과를 넣어준다.
- s1과 s2가 문자 로그인 경우, 내용이 같지 않은 경우 s1의 내용과 s2의 내용을 비교한 값을 아니면 식별자까지 포함한 s1과 s2을 비교한 값을 반환한다.
- s1만 문자 로그이면 -1을, s2만 문자 로그이면 1을, 둘 다 숫자 로그이면 0을 반환한다.

3. 위를 통해 정렬된 logs를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReorderDataInLogFiles.java){:target="_blank"}에서 확인 가능합니다.