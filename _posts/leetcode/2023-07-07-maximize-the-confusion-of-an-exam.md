---
title: "Leetcode Java Maximize the Confusion of an Exam"
excerpt: "Leetcode Maximize the Confusion of an Exam Java"
last_modified_at: 2023-07-07T20:10:00
header:
  image: /assets/images/leetcode/maximize-the-confusion-of-an-exam.png
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
[Link](https://leetcode.com/problems/maximize-the-confusion-of-an-exam){:target="_blank"}

# 코드
```java
class Solution {

  public int maxConsecutiveAnswers(String answerKey, int k) {
    int max = 0;
    int i = 0;
    char[] charArray = answerKey.toCharArray();
    int length = charArray.length;
    int[] count = new int[26];
    for (int j = 0; j < length; j++) {
      max = Math.max(max, ++count[charArray[j] - 'A']);
      if (j - i + 1 > max + k) {
        --count[charArray[i++] - 'A'];
      }
    }
    return length - i;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximize-the-confusion-of-an-exam/submissions/988513311/){:target="_blank"}

# 설명
1. 'T'와 'F'로 이루어진 answerKey의 문자열 중 k개의 문자의 값을 변환하여 만들 수 있는 동일한 문자열로 구성된 최대 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- max는 최댓값을 저장시키기 위한 변수로, 0으로 초기화한다.
- i는 연속된 문자열을 나열했을 경우 길이를 측정하기 위한 위치 변수로, 0으로 초기화한다.
- charArray는 answerKey를 문자 배열로 변환한 변수이다.
- length는 charArray의 길이를 저장한 변수이다.
- count는 각 문자 별 갯수를 저장할 변수이다.

3. 0부터 length 미만까지 j를 증가시키며 아래를 수행한다.
- max에 max와 count의 j번째 문자의 길이를 증가시킨 값 중 큰 값을 넣어준다.
- $j - i + 1$인 연속된 문자의 길이가 $max + k$인 최대 문자 길이에 k번 변경했을 경우보다 큰 경우, count의 i번째 문자의 위치의 값을 감소시킨다.

4. 반복이 완료되면 length에 i를 뺀 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximizeTheConfusionOfAnExam.java){:target="_blank"}에서 확인 가능합니다.