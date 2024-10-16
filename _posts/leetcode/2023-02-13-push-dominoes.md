---
title: "Leetcode Java Push Dominoes"
excerpt: "Leetcode Push Dominoes Java"
last_modified_at: 2023-02-13T19:00:00
header:
  image: /assets/images/leetcode/push-dominoes.png
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
[Link](https://leetcode.com/problems/push-dominoes){:target="_blank"}

# 코드
```java
class Solution {

  public String pushDominoes(String dominoes) {
    char[] charArray = dominoes.toCharArray();
    int index = -1;
    char c = '.';
    for (int idx = 0; idx < charArray.length; idx++) {
      if (charArray[idx] == 'L') {
        if (index == -1 || c == 'L') {
          while (index < idx - 1) {
            charArray[++index] = 'L';
          }
        } else if (c == 'R') {
          int left = index + 1;
          int right = idx - 1;
          while (left < right) {
            charArray[left++] = 'R';
            charArray[right--] = 'L';
          }
        }
        index = idx;
        c = 'L';
      } else if (charArray[idx] == 'R') {
        if (c == 'R') {
          while (index < idx - 1) {
            charArray[++index] = 'R';
          }
        }
        index = idx;
        c = 'R';
      }
    }
    if (c == 'R') {
      while (index < charArray.length - 1) {
        charArray[++index] = 'R';
      }
    }
    return String.valueOf(charArray);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/push-dominoes/submissions/897093663/){:target="_blank"}

# 설명
1. 일렬로 세워둔 dominoes를 이용하여 좌측인 'L'과 우측인 'R'로 밀었을 때, 도미노가 쓰러진 형태를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 dominoes를 문자 배열로 변환하여 저장한 변수이다.
- index와 c는 위치와 문자를 저장하기 위한 변수로, -1과 '.'으로 초기화한다.

3. 0부터 charArray의 길이 미만까지 idx를 증가시키며 아래를 반복한다.
- charArray의 idx번째 문자가 'L'인 경우, 아래를 수행한다.
  - index가 -1이거나 c가 'L'인 경우, index가 $idx - 1$ 미만일 때 까지 index를 증가시키며 charArray의 index번째 위치에 'L'을 넣어 좌측으로 쓰러진 도미노의 값을 넣어준다.
  - c가 'R'이면 left에 $index + 1$을, right를 $idx - 1$을, left가 right 미만까지 left를 증가시키며 charArray의 left번째 위치에 'R'을, right를 감소시키며 charArray의 right번쨰 위치에 'L'을 넣어 좌우로 도미노가 넘어지는 값을 넣어준다.
  - index에 idx를 넣고, c에 'L'을 기록해준다.
- charArray의 idx번째 문자가 'R'인 경우, 아래를 수행한다.
  - c가 'R'이면 index가 $idx - 1$ 미만까지 index를 증가시키며 charArray의 index번째 위치에 'R'을 넣어 오른쪽으로 쓰러진 도미노의 값을 넣어준다.
  - index에 idx르 넣고, c에 'R'을 기록해준다.

4. c가 'R'인 경우, index가 charArray의 길이보다 1 작을 때 까지 반복하여 index를 증가시키며 charArray의 index번째 값에 'R'을 넣어 우측으로 쓰러진 도미노의 값을 넣어준다.

5. 마지막으로 charArray를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PushDominoes.java){:target="_blank"}에서 확인 가능합니다.