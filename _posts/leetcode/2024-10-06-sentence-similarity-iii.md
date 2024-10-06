---
title: "Leetcode Java Sentence Similarity III"
excerpt: "Leetcode Sentence Similarity III Java"
last_modified_at: 2024-10-06T10:50:00
header:
  image: /assets/images/leetcode/sentence-similarity-iii.png
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
[Link](https://leetcode.com/problems/sentence-similarity-iii/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean areSentencesSimilar(String sentence1, String sentence2) {
    String[] words1 = sentence1.split(" ");
    String[] words2 = sentence2.split(" ");
    int length1 = words1.length;
    int length2 = words2.length;
    if (length1 == length2) {
      for (int i = 0; i < length1; i++) {
        if (!words1[i].equals(words2[i])) {
          return false;
        }
      }
      return true;
    }
    int i = 0;
    int j = 0;
    while (i < length1 && i < length2 && words1[i].equals(words2[i])) {
      i++;
    }
    while (j < length1 - i && j < length2 - i && words1[length1 - 1 - j].equals(words2[length2 - 1 - j])) {
      j++;
    }
    return i + j >= Math.min(length1, length2);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sentence-similarity-iii/submissions/1413139314/){:target="_blank"}

# 설명
1. sentence1에 특정 문자열을 추가할 때 sentence2를 만들 수 있는지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- words1과 words2는 sentence1과 sentence2를 공백 문자(" ") 기준으로 분리한 문자열을 저장한 변수이다.
- length1과 length2는 sentence1과 sentence2의 길이를 저장한 변수이다.

3. length1과 length2가 같은 경우, 각 문자열이 동일한지 여부를 주어진 문제의 결과로 반환한다.

4. i와 j는 동일한 문자열 탐색에 필요한 변수로, 0으로 초기화한다.

5. i는 length1와 length2 미만이면서 words1와 words2의 동일한 문자열의 갯수를 계산한다.

6. j는 문자열의 마지막 위치인 $length1 - i$과 $length2 - i$ 미만이면서 words1와 words2의 마지막 문자열 부터 동일한 문자열의 갯수를 계산한다.

7. 아래의 각 경우에 대한 결과를 주어진 문제의 결과로 반환한다.
- $i + j$가 length1과 length2 중 작은 값보다 큰 경우, 문자열을 추가하여 만들 수 있으므로 true를 주어진 문제의 결과로 반환한다.
- $i + j$가 length1과 length2 중 작은 값보다 작거나 같은 경우, 문자열이 다르거나 만들 수 없으므로 false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SentenceSimilarityIII.java){:target="_blank"}에서 확인 가능합니다.