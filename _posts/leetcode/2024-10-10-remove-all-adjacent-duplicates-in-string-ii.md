---
title: "Leetcode Java Remove All Adjacent Duplicates in String II"
excerpt: "Leetcode Remove All Adjacent Duplicates in String II Java"
last_modified_at: 2024-10-10T18:30:00
header:
  image: /assets/images/leetcode/remove-all-adjacent-duplicates-in-string-ii.png
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
[Link](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public String removeDuplicates(String s, int k) {
    int[] count = new int[s.length()];
    StringBuilder sb = new StringBuilder();
    for (char c : s.toCharArray()) {
      sb.append(c);
      int length = sb.length();
      int i = length - 1;
      count[i] = 1 + (i > 0 && sb.charAt(i) == sb.charAt(i - 1) ? count[i - 1] : 0);
      if (count[i] >= k) {
        sb.delete(length - k, length);
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/submissions/1417886947/){:target="_blank"}

# 설명
1. 문자열 s에서 k번 반복되는 문자열을 모두 제거한 문자열을 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 문자열 갯수를 계산할 변수로, 최대 길이인 문자열 s의 길이로 초기화한다.
- sb는 동적으로 문자열 생성하기 위한 변수로, StringBuilder로 초기화한다.

3. s의 문자들을 순차적으로 c에 넣어 아래를 반복한다.
- sb에 c를 넣어준다.
- length에 sb의 길이를 넣고, i에 $length - 1$인 sb 마지막 위치를 넣어준다.
- count[i]에 1과 아래의 경우에 따른 값을 더한 값을 넣어준다.
  - i가 0보다 크면서 sb의 i번째 위치의 문자가 이전과 동일한 경우 이전 연속된 값인, count[$i - 1$]을 더하여 갯수를 증가시켜준다.
  - 위의 경우가 아니라면 0을 넣어 값을 초기화한다.
- count[i]가 k 이상인 경우, sb에서 $length - k$번째 위치부터 length까지 문자들을 제거한다.

4. 반복이 완료되어 완성된 sb를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveAllAdjacentDuplicatesInStringII.java){:target="_blank"}에서 확인 가능합니다.