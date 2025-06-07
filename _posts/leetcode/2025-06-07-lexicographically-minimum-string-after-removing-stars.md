---
title: "Leetcode Java Lexicographically Minimum String After Removing Stars"
excerpt: "Leetcode - 'Lexicographically Minimum String After Removing Stars' 문제 Java 풀이"
last_modified_at: 2025-06-07T11:20:00
header:
  image: /assets/images/leetcode/lexicographically-minimum-string-after-removing-stars.png
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
[Link](https://leetcode.com/problems/lexicographically-minimum-string-after-removing-stars/){:target="_blank"}

# 코드
```java
class Solution {

  public String clearStars(String s) {
    char[] charArray = s.toCharArray();
    int length = charArray.length;
    List<List<Integer>> lists = new ArrayList<>();
    for (int i = 0; i < 26; i++) {
      lists.add(new ArrayList<>());
    }
    boolean[] removed = new boolean[length];
    for (int i = 0; i < length; i++) {
      if (charArray[i] == '*') {
        removed[i] = true;
        for (int j = 0; j < 26; j++) {
          List<Integer> list = lists.get(j);
          if (!list.isEmpty()) {
            int last = list.size() - 1;
            removed[list.get(last)] = true;
            list.remove(last);
            break;
          }
        }
      } else {
        lists.get(charArray[i] - 'a').add(i);
      }
    }
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < length; i++) {
      if (!removed[i]) {
        sb.append(charArray[i]);
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/lexicographically-minimum-string-after-removing-stars/submissions/1656122338/){:target="_blank"}

# 설명
1. 문자열 s에서 아래의 절차를 반복 수행한 후 사전적 순서가 가장 작은 문자열을 만드는 문제이다.
- 현재 문자열에서 '\*'문자가 존재하는 경우, 해당 문자와 '\*' 문자가 아닌 좌측에 존재하는 가장 작은 문자 중 하나를 반복하여 제거한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 문자열 s를 문자 배열로 저장한 변수이다.
- length는 charArray의 길이를 저장한 변수이다.
- lists는 각 문자들의 위치를 순차적으로 저장할 변수로, ArrayList로 초기화 후 영문자 갯수인 26개의 ArrayList를 다시 넣어준다.
- removed는 제거된 문자인지 기록하기 위한 변수로, length 길이의 부울 배열로 초기화한다.

3. 0부터 length 미만까지 i를 증가시킨다.
- charArray의 i번째 문자가 '/*'인 경우, 아래를 수행한다.
  - removed[i]의 값을 true로 변경하여 제거된 문자임을 체크해준다.
  - 0부터 26 미만까지 j를 증가시키며, list에 lists의 i번째 ArrayList를 넣어준 후 removed 내 list의 마지막 값에 해당하는 위치의 값을 true로 바꾼 후 list의 last번째 값을 제거하고 반복을 중지한다.
- charArray의 i번째 문자가 '/*'가 아닌 경우, lists의 charArray의 i번째 문자 위치의 ArrayList에 i인 위치를 넣어준다.

4. sb는 사전적 순서가 가장 작은 문자열을 만들기 위한 변수로, 0부터 length 미만까지 i를 증가시키며 제거된 문자가 아닌 경우만 sb에 순차적으로 넣어준다.

5. 4번을 통해 제거된 문자를 제외하고 사전적 순서가 작은 문자들을 순차적으로 넣은 sb를 문자열로 변환하여  주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LexicographicallyMinimumStringAfterRemovingStars.java){:target="_blank"}에서 확인 가능합니다.