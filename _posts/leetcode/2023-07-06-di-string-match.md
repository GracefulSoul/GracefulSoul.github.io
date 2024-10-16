---
title: "Leetcode Java DI String Match"
excerpt: "Leetcode DI String Match Java"
last_modified_at: 2023-07-06T18:20:00
header:
  image: /assets/images/leetcode/di-string-match.png
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
[Link](https://leetcode.com/problems/di-string-match){:target="_blank"}

# 코드
```java
class Solution {

  public int[] diStringMatch(String s) {
    int length = s.length();
    int left = 0;
    int right = length;
    int[] result = new int[length + 1];
    for (int i = 0; i < length; i++) {
      result[i] = s.charAt(i) == 'I' ? left++ : right--;
    }
    result[s.length()] = left;
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/di-string-match/submissions/987644810/){:target="_blank"}

# 설명
1. s를 이용하여 아래의 규칙을 만족하는 0부터 s의 길이까지 범위의 값으로 구성된 배열을 구성하는 문제이다.
- s의 i번째 문자가 'I'인 경우, perm[i] < perm[i + 1]을 만족한다.
- s의 i번째 문자가 'D'인 경우, perm[i] > perm[i + 1]을 만족한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 s의 길이를 저장한 변수이다.
- left와 right는 문자열의 탐색에 필요한 변수로, 0과 length로 초기화한다.
- result는 규칙을 만족하는 배열을 구성하기 위한 변수로, $length + 1$ 크기의 정수 배열로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 수행한다.
- s의 i번째 문자가 'I'인 경우, result의 i번째 위치에 left를 넣고 left를 증가신다.
- s의 i번째 문자가 'D'인 경우, result의 i번째 위치에 right를 넣고 right를 감소시킨다.

4. result의 마지막 위치에 left를 넣어주고, 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DIStringMatch.java){:target="_blank"}에서 확인 가능합니다.