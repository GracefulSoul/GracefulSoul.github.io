---
title: "Leetcode Java Remove Comments"
excerpt: "Leetcode Remove Comments Java"
last_modified_at: 2022-11-11T19:50:00
header:
  image: /assets/images/leetcode/remove-comments.png
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
[Link](https://leetcode.com/problems/remove-comments){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> removeComments(String[] source) {
    List<String> result = new ArrayList<>();
    StringBuilder sb = new StringBuilder();
    boolean inBlock = false;
    for (String line : source) {
      for (int idx = 0; idx < line.length(); idx++) {
        if (!inBlock) {
          if (line.charAt(idx) == '/' && idx + 1 < line.length() && line.charAt(idx + 1) == '/') {
            break;
          }
          if (line.charAt(idx) == '/' && idx + 1 < line.length() && line.charAt(idx + 1) == '*') {
            inBlock = true;
            idx++;
          } else {
            sb.append(line.charAt(idx));
          }
        } else {
          if (line.charAt(idx) == '*' && idx + 1 < line.length() && line.charAt(idx + 1) == '/') {
            idx++;
            inBlock = false;
          }
        }
      }
      if (!inBlock && sb.length() > 0) {
        result.add(sb.toString());
        sb.setLength(0);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/841308029/){:target="_blank"}

# 설명
1. 소스 코드의 라인을 배열로 저장한 source를 이용하여 주석을 제거하는 문제이다.
- 문자열 "//"의 경우, 해당 문자열 우측의 모든 내용이 주석이므로 제거한다.
- 문자열 "/*"의 경우, "*/"의 문자열이 존재하면 두 문자열 사이의 모든 문자열이 주석이므로 제거한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 주석을 제거한 소스 코드를 저장할 변수로, ArrayList로 초기화한다.
- sb는 주석을 제거한 문자열을 만들 변수로, 동적 문자열을 효율적으로 생성하기 위해 StringBuilder로 초기화한다.
- inBlock은 주석에 포함되는 영역을 구분하기 위한 변수로, false로 초기화한다.

3. source의 모든 문자열들을 line에 넣어 아래를 반복한다.
- 0부터 line의 길이 이전까지 idx를 증가시키며 아래를 수행한다.
  - inBlock이 false인 경우, 문자열 "//"이 시작하는 위치이면 반복을 중단하고 문자열 "/\*"이 시작하는 위치이면 inBlock을 true로 바꾸어 주석 시작을 체크하고 idx를 증가시켜 주석 내 문장 위치로 이동한다.
  - inBlock이 아니면서 위의 문자열 "//"과 "/\*"이 아닌 경우 소스 코드이므로, sb에 line의 idx번째 문자를 넣어준다.
  - inBlock이 true이면서 "\*/"문자열의 위치인 경우, idx를 증가시켜 주석 영역 밖으로 이동시키고 inBlock을 false로 바꾸어 주석 영역을 종료한다.

4. 반복이 종료되면 주석을 제거한 문자열을 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveComments.java){:target="_blank"}에서 확인 가능합니다.