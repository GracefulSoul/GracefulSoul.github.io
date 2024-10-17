---
title: "Leetcode Java Compare Strings by Frequency of the Smallest Character"
excerpt: "Leetcode Medium - 'Compare Strings by Frequency of the Smallest Character' 문제 Java 풀이"
last_modified_at: 2024-08-23T21:20:00
header:
  image: /assets/images/leetcode/compare-strings-by-frequency-of-the-smallest-character.png
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
[Link](https://leetcode.com/problems/compare-strings-by-frequency-of-the-smallest-character/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] numSmallerByFrequency(String[] queries, String[] words) {
    int[] counts = new int[11];
    for (String word : words) {
      counts[this.getCount(word)]++;
    }
    for (int i = 0; i < counts.length - 1; i++) {
      counts[i + 1] += counts[i];
    }
    int[] result = new int[queries.length];
    for (int i = 0; i < queries.length; i++) {
      result[i] = counts[counts.length - 1] - counts[this.getCount(queries[i])];
    }
    return result;
  }

  private int getCount(String word) {
    int[] counts = new int[26];
    for (char c : word.toCharArray()) {
      counts[c - 'a']++;
    }
    for (int count : counts) {
      if (count != 0) {
        return count;
      }
    }
    return 0;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/compare-strings-by-frequency-of-the-smallest-character/submissions/1365690668/){:target="_blank"}

# 설명
1. f(s)는 문자열 s의 사전적 순서가 가장 작은 문자의 갯수를 반환하는 함수로, words의 각 문자열 W에 대해 $f(query[i]) < f(W)$를 만족하는 갯수를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- counts는 words 내 사전적 순서가 가장 작은 문자의 갯수를 계산할 변수로, words의 최대 갯수보다 큰 11 크기의 정수 배열로 초기화 후 아래를 수행한다.
  - words의 문자를 반복하여 사전적 순서가 작은 문자의 갯수에 해당하는 위치의 값을 증가시킨다.
  - counts를 순차적으로 다음 위치에 현재 위치 값을 더한 누계를 합산해준다.
- result는 $f(query[i]) < f(W)$를 만족하는 갯수를 저장할 변수로, queries의 크기와 동일한 정수 배열로 초기화한다.

3. 0부터 queries의 크기 미만까지 i를 증가시키며 아래를 수행한다.
- result[i]에 counts의 마지막 값에서 counts의 queries[i]의 사전적 순서가 작은 위치의 값을 뺀, words 중 사전적 순서가 queries[i]보다 큰 갯수를 넣어준다.

4. 반복이 완료되어 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CompareStringsByFrequencyOfTheSmallestCharacter.java){:target="_blank"}에서 확인 가능합니다.