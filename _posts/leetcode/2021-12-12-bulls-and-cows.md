---
title: "Leetcode Java Bulls and Cows"
excerpt: "Leetcode Bulls and Cows Java 풀이"
last_modified_at: 2021-12-12T12:00:00
header:
  image: /assets/images/leetcode/bulls-and-cows.png
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
[Link](https://leetcode.com/problems/bulls-and-cows/){:target="_blank"}

# 코드
```java
class Solution {

  public String getHint(String secret, String guess) {
    int bulls = 0;
    int cows = 0;
    int[] count = new int[10];
    for (int idx = 0; idx < secret.length(); idx++) {
      char secretChar = secret.charAt(idx);
      char guessChar = guess.charAt(idx);
      if (secretChar == guessChar) {
        bulls++;
      } else {
        if (count[secretChar - '0']++ < 0) {
          cows++;
        }
        if (count[guessChar - '0']-- > 0) {
          cows++;
        }
      }
    }
    return new StringBuilder().append(bulls).append("A").append(cows).append("B").toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/600493562/){:target="_blank"}

# 설명
1. [Bulls And Cows](https://en.wikipedia.org/wiki/Bulls_and_Cows){:target="_blank"} 게임을 하는 문제이다.
- 비밀 숫자인 secret을 맞추기 위해 추측값 guess를 제시하면 해당 값에 대한 결과를 x개의 "황소"와 y개의 "소"를 xAyB형태로 반환한다.
- "황소"란 정확한 위치에 있는 추측의 숫자의 개수를 의미한다.
- "소"란 비밀 숫자에 포함되어 있지만, 잘못된 위치에 있는 추측의 숫자의 개수를 의미한다.
- 단 y의 경우 중복된 숫자를 제외하고 표기한다.
  - secret = 1123, guess = 0111인 경우, 소는 3번째와 4번째의 1이지만 1A1B로 표기한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- bulls는 황소의 숫자를 세기 위한 변수로, 0으로 초기화한다.
- cows는 소의 숫자를 세기 위한 변수로, 0으로 초기화한다.
- count는 각 숫자를 개수를 세기 위한 배열로, 0 ~ 9까지 존재하므로 크기를 10으로 설정하여 초기화한다.

3. secret의 길이만큼 반복하여 호아소와 소의 개수를 센다.
- secret의 idx번째 문자를 secretChar에 넣어준다.
- guess의 idx번째 문자를 guessChar에 넣어준다.
- secretChar와 guessChar가 동일하다면 bulls를 증가시킨다.
- 동일하지 않다면, 아래를 수행한다.
  - ASCII 값을 활용하여 secretChar의 숫자에 해당하는 count 내 해당 위치의 값이 0보다 작으면 guess에 포함된 숫자이므로 cows를 증가시키고, 해당 여부와 상관없이 cow를 증가시켰으니 count내 해당 위치의 값을 증가시켜준다.
  - ASCII 값을 활용하여 guessChar의 숫자에 해당하는 count 내 해당 위치의 값이 0보다 크면 secret에 포함된 숫자이므로 cows를 증가시키고, 해당 여부와 상관없이 cow를 증가시켰으니 count내 해당 위치의 값을 증가시켜준다.

4. 반복을 통해 bulls와 cows를 모두 확인하였으면, 해당 값을 이용하여 xAyB형태의 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BullsAndCows.java){:target="_blank"}에서 확인 가능합니다.