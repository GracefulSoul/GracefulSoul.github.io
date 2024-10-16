---
title: "Leetcode Java Reconstruct Original Digits from English"
excerpt: "Leetcode Reconstruct Original Digits from English Java 풀이"
last_modified_at: 2022-03-20T12:00:00
header:
  image: /assets/images/leetcode/reconstruct-original-digits-from-english.png
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
[Link](https://leetcode.com/problems/reconstruct-original-digits-from-english/){:target="_blank"}

# 코드
```java
class Solution {

  public String originalDigits(String s) {
    char[] charCount = new char['a' + 26];
    for (char c : s.toCharArray()) {
      charCount[c]++;
    }
    int[] count = new int[10];
    count[0] = charCount['z'];
    count[2] = charCount['w'];
    count[4] = charCount['u'];
    count[6] = charCount['x'];
    count[8] = charCount['g'];
    count[3] = charCount['h'] - count[8];
    count[5] = charCount['f'] - count[4];
    count[7] = charCount['s'] - count[6];
    count[9] = charCount['i'] - count[6] - count[5] - count[8];
    count[1] = charCount['n'] - count[7] - (2 * count[9]);
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < 10; i++) {
      for (int j = 0; j < count[i]; j++) {
        sb.append(i);
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/663438039/){:target="_blank"}

# 설명
1. 주어진 문자열 s가 주어지면 해당 문자열 기반으로 영문 숫자를 만들 수 있는 숫자들을 오름차순으로 변환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charCount는 문자열 s에 포함된 영문자의 개수를 저장할 변수로, 'a'의 ASCII 코드 값에 'z'까지 넣기 위해 26을 더해서 정의하고 문자열 s를 반복하여 영문자의 개수를 넣어준다.
- count는 생성 가능한 0부터 9까지의 숫자 개수를 저장하기 위한 변수로, 숫자의 개수인 10 크기로 초기화한다.

3. 생성 가능한 숫자를 count 배열에 추가한다.
- 0 ~ 9 까지 영문자 중 고유하게 생성 가능한 영문자들의 개수를 먼저 센다.
- 간단히 0 ~ 9 까지 숫자를 영문자로 변환해보면 아래와 같다.
- |:--------|:--------|
| 0 | zero |
| 1 | one |
| 2 | two |
| 3 | three |
| 4 | four |
| 5 | five |
| 6 | six |
| 7 | seven |
| 8 | eight |
| 9 | nine |
- <b>z</b>ero, t<b>w</b>o, fo<b>u</b>r, si<b>x</b>, ei<b>g</b>ht는 다른 숫자의 영문자 내 포함되지 않으므로 count의 각 숫자 위치에 charCount에서 굵은 영문자에 해당하는 ASCII 코드 값의 위치 값을 넣어준다.
- 그 다음 계산이 필요한 항목들을 아래와 같이 계산한다.
  - t<b>h</b>ree의 경우, eig<b>h</b>t가 존재하기 때문에 count[3]에 charCount에서 'h'의 ASCII 코드 값의 위치 값인 charCount['h']에 count[8]을 뺀 값을 넣어준다.
  - <b>f</b>ive의 경우, <b>f</b>our가 존재하기 때문에 count[5]에 charCount에서 'f'의 ASCII 코드 값의 위치 값인 charCount['f']에 count[4]을 뺀 값을 넣어준다.
  - <b>s</b>even의 경우, <b>s</b>ix가 존재하기 때문에 count[7]에 charCount에서 's'의 ASCII 코드 값의 위치 값인 charCount['s']에 count[6]을 뺀 값을 넣어준다.
  - n<b>i</b>ne의 경우, f<b>i</b>ve와 s<b>i</b>x, e<b>i</b>ght가 존재하기 때문에 count[9]에 charCount에서 'i'의 ASCII 코드 값의 위치 값인 charCount['i']에 count[5], count[6], count[8]의 값들을 빼준다.
  - o<b>n</b>e의 경우, seve<b>n</b>과 <b>n</b>i<b>n</b>e이 존재하기 때문에 count[1]에 charCount에서 'n'의 ASCII 코드 값의 위치 값인 charCount['n']에 count[7]의 값을 빼고 9에는 n이 2개 들어가므로 count[9]는 2배로 빼준다.

4. 숫자를 오름차순 문자열로 만들어 생성하기위한 sb를 StringBuilder로 초기화한다.
- 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.

5. 0부터 9까지 i를 증가시키며 반복한다.
- 0부터 count[i]의 값까지 j를 증가시키며, sb에 j의 수만큼 반복하여 i를 넣어준다.

6. 반복이 완료되면 문자열 s를 오름차순의 숫자를 이어준 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReconstructOriginalDigitsFromEnglish.java){:target="_blank"}에서 확인 가능합니다.