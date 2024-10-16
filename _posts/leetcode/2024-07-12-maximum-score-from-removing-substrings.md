---
title: "Leetcode Java Maximum Score From Removing Substrings"
excerpt: "Leetcode Maximum Score From Removing Substrings Java"
last_modified_at: 2024-07-12T17:30:00
header:
  image: /assets/images/leetcode/maximum-score-from-removing-substrings.png
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
[Link](https://leetcode.com/problems/maximum-score-from-removing-substrings/){:target="_blank"}

# 코드
```java
class Solution {

  public int maximumGain(String s, int x, int y) {
    StringBuilder sb = new StringBuilder(s);
    if (x > y) {
      return this.maximumGain(sb, "ab", x) + this.maximumGain(sb, "ba", y);
    } else {
      return this.maximumGain(sb, "ba", y) + this.maximumGain(sb, "ab", x);
    }
  }

  private int maximumGain(StringBuilder sb, String keyword, int point) {
    int result = 0;
    int i = 0;
    for (int j = 0; j < sb.length(); j++) {
      sb.setCharAt(i++, sb.charAt(j));
      if (i > 1 && keyword.equals(sb.substring(i - 2, i))) {
        i -= 2;
        result += point;
      }
    }
    sb.setLength(i);
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-score-from-removing-substrings/submissions/1318442916/){:target="_blank"}

# 설명
1. 문자열 s에서 아래 규칙대로 수행하여 발생할 수 있는 최대 점수를 구하는 문제이다.
- s에서 "ab" 문자열을 제거하는 경우, x 점수를 얻는다.
- s에서 "ba" 문자열을 제거하는 경우, y 점수를 얻는다.

2. sb는 동적으로 문자열 제거를 위한 변수로, StringBuilder에 s를 넣어 초기화한다.

3. x가 y보다 크면 "ab"를 변환한 점수가 더 크므로 "ab" -> "ba" 순으로, 아니면 "ba"를 변환한 점수가 더 크거나 같으므로 "ba" -> "ab" 순으로 4번에서 정의한 maximumGain(StringBuilder sb, String keyword, int point) 메서드를 수행한 결과를 주어진 문제의 결과로 반환한다.

4. 문자열에서 키워드별 점수를 계산하기 위한 maximumGain(StringBuilder sb, String keyword, int point) 메서드를 정의한다.
- 점수 계산에 필요한 변수를 정의한다.
  - result는 점수의 합계를 위한 변수로, 0으로 초기화한다.
  - i는 수정한 문자열의 마지막 위치를 저장할 변수로, 0으로 초기화한다.
- 0부터 sb의 길이 미만까지 j를 증가시키면서 아래를 수행한다.
  - sb의 i번째 위치에 j번째 문자를 넣어 순서를 당겨주고 i를 증가시켜준다.
  - i가 1 초과이면서 keyword와 sb의 $i - 2$ 위치의 두 문자가 동일하면, i를 2 감소시켜 해당 문자열을 삭제하고 result에 point를 더해 점수를 계산해준다.
- 반복이 완료되면 sb에 최종 문자열 길이인 i를 넣어 문자열을 수정해주고, 계산된 점수인 result를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumScoreFromRemovingSubstrings.java){:target="_blank"}에서 확인 가능합니다.