---
title: "Leetcode Java Maximum Manhattan Distance After K Changes"
excerpt: "Leetcode - 'Maximum Manhattan Distance After K Changes' 문제 Java 풀이"
last_modified_at: 2025-06-21T21:20:00
header:
  image: /assets/images/leetcode/minimum-deletions-to-make-string-k-special.png
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
[Link](https://leetcode.com/problems/minimum-deletions-to-make-string-k-special/){:target="_blank"}

# 코드
```java
class Solution {

  public int minimumDeletions(String word, int k) {
    int result = 100000;
    int[] counts = new int[26];
    for (char c : word.toCharArray()) {
      counts[c - 'a']++;
    }
    for (int i = 0; i < 26; i++) {
      if (counts[i] == 0) {
        continue;
      }
      int count = 0;
      for (int j = 0; j < 26; j++) {
        if (i == j || counts[j] == 0) {
          continue;
        }
        count += counts[j] < counts[i] ? counts[j] : Math.max(0, counts[j] - (counts[i] + k));
      }
      result = Math.min(result, count);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-deletions-to-make-string-k-special/submissions/1671484565/){:target="_blank"}

# 설명
1. word 내 문자의 각 갯수가 모두 k개 이내의 차이가 되도록 하기 위해 삭제해야 할 문자의 최소 갯수를 게산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 삭제할 문자의 갯수르 계산하기위한 변수로, 문자열의 최대 길이인 $10^5$로 초기화한다.
- counts는 word의 각 문자 갯수를 계산하여 저장할 변수로, word의 각 문자 별 위치에 해당 갯수를 넣어준다.

3. 0부터 26 미만까지 i를 증가시키며 아래를 반복한다.
- counts[i]의 값이 0인 존재하지 않는 경우는 무시한다.
- count는 현재 삭제할 문자의 갯수를 저장할 변수로, 0으로 초기화한다.
- 0부터 26 미만까지 j를 증가시키며 아래를 반복한다.
  - i와 j가 동일한 검증이 필요 없거나, counts[j]의 값이 0인 존재하지 않는 문자의 경우는 무시한다.
  - count에 counts[j]의 값이 counts[i]의 값보다 작으면 j번째 문자를 삭제하는 경우인 counts[j]를 넣고, 아니면 0과  k개 이내의 차이가 되기 위한 $counts[j] - (counts[i] + k)$의 값 중 큰 값을 넣어준다.
- 위 반복이 완료되면 result에 아래 두 경우 중 가장 작은 값을 넣어준다.
  - 이전까지 삭제해야할 최소 갯수가 저장된 result의 값.
  - j번째 문자 기준으로 각 문자가 k개 이내의 차이가 되도록 하기 위한 최소 갯수가 저장된 count의 값.

4. 반복이 완료되면 조건을 맍족한 최소 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumDeletionsToMakeStringKSpecial.java){:target="_blank"}에서 확인 가능합니다.