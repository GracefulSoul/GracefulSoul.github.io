---
title: "Leetcode Java Dota2 Senate"
excerpt: "Leetcode Dota2 Senate Java"
last_modified_at: 2022-09-06T12:00:00
header:
  image: /assets/images/leetcode/dota2-senate.png
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
[Link](https://leetcode.com/problems/dota2-senate/){:target="_blank"}

# 코드
```java
class Solution {

  public String predictPartyVictory(String senate) {
    char[] charArray = senate.toCharArray();
    int flag = 0;
    boolean radiant = true;
    boolean dire = true;
    while (radiant && dire) {
      radiant = false;
      dire = false;
      for (int idx = 0; idx < charArray.length; idx++) {
        if (charArray[idx] == 'R') {
          if (flag > 0) {
            charArray[idx] = 'X';
          } else {
            radiant = true;
          }
          flag--;
        } else if (charArray[idx] == 'D') {
          if (flag < 0) {
            charArray[idx] = 'X';
          } else {
            dire = true;
          }
          flag++;
        }
      }
    }
    return radiant ? "Radiant" : "Dire";
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/792595083/){:target="_blank"}

# 설명
1. senate를 이루는 문자를 이용하여 아래의 규칙을 만족하는 경우에 대한 결과를 반환하는 문제이다.
- R과 D는 각각 Radiant와 Dire를 뜻하는 문자이다.
- R이 나온 경우 다음 D를 제거할 수 있고, D가 나온 경우 다음 R을 제거할 수 있다.
- 마지막으로 남아있는 문자를 뜻하는 단어를 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 senate를 문자 배열로 저장한 배열이다.
- flag는 D가 R보다 큰 개수를 저장할 변수로, 0으로 초기화한다.
- radiant와 dire는 이전 자리의 단어가 R인지 D인지를 구분하기 위한 변수로, true로 초기화한다.

3. radiant와 dire 모두 true일 때 까지 아래를 반복한다.
- radiant와 dire를 false로 변경한다.
- 0부터 charArray 길이 미만까지 idx를 증가시키며 아래를 수행한다.
  - charArray의 idx번째 값이 R이면서 flag가 0 초과인 경우, charArray의 idx번째 위치에 X를 넣어 무시해준다.
  - charArray의 idx번째 값이 R이면서 flag가 0 이하인 경우, radiant를 true로 변경해준다.
  - 위를 수행한 이후 flag를 감소시킨다.
  - charArray의 idx번째 값이 D이면서 flag가 0 미만인 경우, charArray의 idx번째 위치에 X를 넣어 무시해준다.
  - charArray의 idx번째 값이 D이면서 flag가 0 이상인 경우, dire를 true로 변경해준다.
  - 위를 수행한 이후 flag를 감소시킨다.

4. 반복이 완료되면 radiant가 true면 Radiant를, 아니면 Dire를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/Dota2Senate.java){:target="_blank"}에서 확인 가능합니다.