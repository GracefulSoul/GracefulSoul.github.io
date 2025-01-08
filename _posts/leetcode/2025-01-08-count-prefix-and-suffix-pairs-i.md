---
title: "Leetcode Java Count Prefix and Suffix Pairs I"
excerpt: "Leetcode - 'Count Prefix and Suffix Pairs I' 문제 Java 풀이"
last_modified_at: 2025-01-08T18:10:00
header:
  image: /assets/images/leetcode/count-prefix-and-suffix-pairs-i.png
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
[Link](https://leetcode.com/problems/count-prefix-and-suffix-pairs-i/){:target="_blank"}

# 코드
```java
class Solution {

  public int countPrefixSuffixPairs(String[] words) {
    int length = words.length;
    int result = 0;
    for (int i = 0; i < length - 1; i++) {
      for (int j = i + 1; j < length; j++) {
        if (words[j].startsWith(words[i]) && words[j].endsWith(words[i])) {
          result++;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-prefix-and-suffix-pairs-i/submissions/1501644637/){:target="_blank"}

# 설명
1. words 내 한 문자가 다른 문자의 접두사이면서 접미사인 조합의 갯수를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 words의 길이를 저장한 변수이다.
- result는 조합의 갯수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 length - 1 미만까지 i를 증가시키면서, $i + 1$부터 length 미만까지 j를 증가시키면서 아래를 반복한다.
- words[j]의 접두사와 접미사가 words[i]인 경우에 result를 증가시켜준다.

4. 반복을 통해 계산된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountPrefixAndSuffixPairsI.java){:target="_blank"}에서 확인 가능합니다.