---
title: "Leetcode Java Word Subsets"
excerpt: "Leetcode Word Subsets Java"
last_modified_at: 2023-05-05T10:00:00
header:
  image: /assets/images/leetcode/word-subsets.png
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
[Link](https://leetcode.com/problems/word-subsets){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> wordSubsets(String[] words1, String[] words2) {
    int[] charArray = new int[26];
    for (String word : words2) {
      int[] temp = new int[26];
      for (char c : word.toCharArray()) {
        int num = c - 'a';
        temp[num]++;
        if (charArray[num] < temp[num]) {
          charArray[num] = temp[num];
        }
      }
    }
    List<String> result = new ArrayList<>();
    for (String word : words1) {
      int[] temp = new int[26];
      for (char c : word.toCharArray()) {
        temp[c - 'a']++;
      }
      if (this.isSubset(charArray, temp)) {
        result.add(word);
      }
    }
    return result;
  }

  private boolean isSubset(int[] charArray, int[] temp) {
    for (int i = 0; i < 26; i++) {
      if (charArray[i] > temp[i]) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/word-subsets/submissions/944655326/){:target="_blank"}

# 설명
1. words2의 각 단어 별 가장 많이 발생한 문자와 갯수가 포함된 words1의 문자열을 탐색하는 문제이다.

2. charArray는 words2의 모든 문자를 포함할 변수로, words2를 반복하여 문자별 가장 큰 문자의 수를 넎어준다.

3. result는 만족하는 문자열을 넣을 변수로, words1을 반복하여 각 문자 별 charArray의 문자와 갯수가 포함되는 문자열만 넣어준다.

4. 모든 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/WordSubsets.java){:target="_blank"}에서 확인 가능합니다.