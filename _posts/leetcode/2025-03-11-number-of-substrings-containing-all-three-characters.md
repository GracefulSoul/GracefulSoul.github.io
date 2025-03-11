---
title: "Leetcode Java Number of Substrings Containing All Three Characters"
excerpt: "Leetcode - 'Number of Substrings Containing All Three Characters' 문제 Java 풀이"
last_modified_at: 2025-03-11T18:30:00
header:
  image: /assets/images/leetcode/number-of-substrings-containing-all-three-characters.png
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
[Link](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/){:target="_blank"}

# 코드
```java
class Solution {

  public int numberOfSubstrings(String s) {
    char[] charArray = s.toCharArray();
    int length = charArray.length;
    int[] lastIndex = new int[] { -1, -1, -1 };
    int result = 0;
    for (int i = 0; i < length; i++) {
      lastIndex[charArray[i] - 'a'] = i;
      result += 1 + Math.min(lastIndex[0], Math.min(lastIndex[1], lastIndex[2]));
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/submissions/1570090687/){:target="_blank"}

# 설명
1. 문자열 s에서 a, b, c 문자가 최소 하나 이상 포함된 연속된 부분 문자열의 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s를 문자 배열로 변환한 변수이다.
- length는 charArray의 길이를 저장한 변수이다.
- lastIndex는 a, b, c 각 위치 별 마지막 위치를 저장할 변수로, 3 크기의 정수 배열로 정의하고 모든 값을 -1로 초기화한다.
- result는 결과인 부분 문자열의 갯수를 계산할 변수로, 0으로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- lastIndex의 charArray[i] 문자에 해당하는 영문자 순서 위치에 i를 넣어준다.
- restul에 lastIndex의 a, b, c 문자에 해당하는 위치 중 가장 작은 값에 1을 더한 값을 더해준다.

4. 반복이 완료되면 부분 문자열의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfSubstringsContainingAllThreeCharacters.java){:target="_blank"}에서 확인 가능합니다.