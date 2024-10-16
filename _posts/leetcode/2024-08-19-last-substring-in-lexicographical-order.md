---
title: "Leetcode Java Last Substring in Lexicographical Order"
excerpt: "Leetcode Last Substring in Lexicographical Order Java"
last_modified_at: 2024-08-19T18:30:00
header:
  image: /assets/images/leetcode/last-substring-in-lexicographical-order.png
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
[Link](https://leetcode.com/problems/last-substring-in-lexicographical-order/){:target="_blank"}

# 코드
```java
class Solution {

  public String lastSubstring(String s) {
    char[] charArray = s.toCharArray();
    int length = charArray.length;
    int i = 0;
    int j = 1;
    int k = 0;
    while (j + k < length) {
      if (charArray[i + k] == charArray[j + k]) {
        k++;
      } else {
        if (charArray[i + k] > charArray[j + k]) {
          j += k + 1;
        } else {
          i = Math.max(i + k + 1, j);
          j = i + 1;
        }
        k = 0;
      }
    }
    return s.substring(i);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/last-substring-in-lexicographical-order/submissions/1361185608/){:target="_blank"}

# 설명
1. 문자열 s의 부분 문자열 중 사전적 순서가 가장 큰 부분 문자열을 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s를 문자 배열로 변환한 변수이다.
- length는 charArray의 길이를 저장한 변수이다.
- i와 j는 부분 문자열 탐색에 필요한 위치 값으로, 0과 1로 초기화한다.
- k는 동일 문자열인 갯수를 넣어 보정치로 사용할 변수로, 0으로 초기화한다.

3. $j + k$가 length 미만일 때까지 아래를 반복한다.
- charArray의 $i + k$번째 문자와 $j + k$번째 문자가 동일한 경우, k를 증가시켜준다.
- 위의 경우가 아니라면 아래의 각 경우 별 수행을 하고 k를 0으로 초기화한다.
  - charArray의 $i + k$번째 문자가 $j + k$번째 문자보다 사전적 순서가 큰 경우, j에 $k + 1$을 더해준다.
  - charArray의 $i + k$번째 문자가 $j + k$번째 문자보다 사전적 순서가 작은 경우, i에 $i + k + 1$과 j 중 큰 값을 넣어주고 j에 $i + 1$을 넣어준다.

4. 반복이 완료되면 s의 사전적 순서가 큰 시작 위치인 i번째 이후 문자열을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LastSubstringInLexicographicalOrder.java){:target="_blank"}에서 확인 가능합니다.