---
title: "Leetcode Java Find the K-th Character in String Game II"
excerpt: "Leetcode - 'Find the K-th Character in String Game II' 문제 Java 풀이"
last_modified_at: 2025-07-04T18:00:00
header:
  image: /assets/images/leetcode/find-the-k-th-character-in-string-game-ii.png
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
[Link](https://leetcode.com/problems/find-the-k-th-character-in-string-game-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public char kthCharacter(long k, int[] operations) {
    int c = 0;
    k--;
    for (int i = 0; k != 0; i++, k >>= 1) {
      c += ((int) (k & 1) & operations[i]);
    }
    return (char) ((c % 26) + 'a');
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-k-th-character-in-string-game-ii/submissions/1685943004/){:target="_blank"}

# 설명
1. 0과 1로 구성된 operations를 이용하여 아래대로 문자열을 만들 때, k번째 문자를 반환하는 문제이다.
- operations[i] 값이 0이면, 현재 단어의 사본을 복사해서 뒤에 이어준다.
- operations[i] 값이 1이면, 현재 단어의 각 문자들을 모두 다음 문자들로 변경 후 기존 문자열 뒤에 이어준다.
- "a" 문자부터 시작해서 현재 문자열 내 모든 영문자들의 다음 순서의 영문자로 변환하여 이어주되, 'z' 문자의 다음 문자는 'a'로 순회한다.
- 예를 들어, "c"에서 연산을 수행하면 "cd"가 되고 "zb"에서 연산을 수행하면 "zbac"가 된다.

2. c는 k번째 문자에 해당하는 영문자 순서를 저장할 변수로, 0으로 초기화한다.

3. k를 감소시킨 후, 0부터 k가 0이 아닐 때 까지 i를 증가시키고, k의 비트를 우측으로 하나씩 이동시키며 아래를 반복한다.
- c에 k와 1의 AND(&) 비트 연산을 수행한 후 operations[i]를 다시 AND(&) 비트 연산을 수행한다.

4. 반복이 완료되면 c를 26으로 나눈 나머지 값에 'a'문자를 추가 후 문자로 변환하여 주어진 문제의 결과로 반환한다.

# 해설
- k를 1 감소시켜 0-index 기반으로 변환해준 후 만들어지는 문자열 s의 k번째 문자를 찾을 수 있도록 한다.
- operations[i] 값에 따라 아래의 경우를 고려한다.
  - operations[i]의 값이 0인 경우, 동일한 문자열이 반복해서 이어진다.
  - operations[i]의 값이 1인 경우, 이어지는 문자열은 이전 문자들보다 하나 씩 큰 문자들로 이어진다.
- 위를 통해서 k의 i번째 비트가 1인 경우, operations[i]를 적용한 후 합계가 더해진 c를 영소문자 갯수인 26으로 나눈 나머지 값을 영소문자로 변환하여 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindTheKthCharacterInStringGameII.java){:target="_blank"}에서 확인 가능합니다.