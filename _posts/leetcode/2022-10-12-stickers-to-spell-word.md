---
title: "Leetcode Java Stickers to Spell Word"
excerpt: "Leetcode Stickers to Spell Word Java"
last_modified_at: 2022-10-12T20:07:00
header:
  image: /assets/images/leetcode/stickers-to-spell-word.png
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
[Link](https://leetcode.com/problems/stickers-to-spell-word){:target="_blank"}

# 코드
```java
class Solution {

  public int minStickers(String[] stickers, String target) {
    int length = stickers.length;
    int[][] dp = new int[length][26];
    for (int idx = 0; idx < length; idx++) {
      for (char c : stickers[idx].toCharArray()) {
        dp[idx][c - 'a']++;
      }
    }
    Map<String, Integer> map = new HashMap<>();
    map.put("", 0);
    return this.recursive(dp, target, map);
  }

  private int recursive(int[][] dp, String target, Map<String, Integer> map) {
    if (map.containsKey(target)) {
      return map.get(target);
    }
    int min = Integer.MAX_VALUE;
    int length = dp.length;
    int[] str = new int[26];
    for (char c : target.toCharArray()) {
      str[c - 'a']++;
    }
    for (int i = 0; i < length; i++) {
      if (dp[i][target.charAt(0) - 'a'] == 0) {
        continue;
      }
      StringBuilder sb = new StringBuilder();
      for (int j = 0; j < 26; j++) {
        if (str[j] > 0) {
          for (int k = 0; k < Math.max(0, str[j] - dp[i][j]); k++) {
            sb.append((char) (j + 'a'));
          }
        }
      }
      int temp = this.recursive(dp, sb.toString(), map);
      if (temp != -1) {
        min = Math.min(min, 1 + temp);
      }
    }
    map.put(target, min == Integer.MAX_VALUE ? -1 : min);
    return map.get(target);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/820818476/){:target="_blank"}

# 설명
1. stickers의 문자들을 이용하여 target 문자열을 만드는데 필요한 최소 stickers의 갯수를 구하는 문제이다.
- stickers의 특정 문자열을 이용하여 target을 만들고 다시 정렬하여 나머지 문자를 이어 완성한다.
- 단, 만들 수 없을 결우 -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 stickers의 길이를 저장한 변수이다.
- dp는 stickers의 문자들을 저장할 변수로, length의 길이와 영문자의 갯수인 $length \times 26$ 크기로 초기화하고 stickers를 차례대로 반복하여 모든 문자들을 기록해준다.
- map은 각 문자열의 만들 수 있는 stickers 내 문자열 갯수를 저장할 변수로, HashMap으로 초기화하고 빈 값에 매치할 값을 0으로 넣어준다.

3. 4번에서 정의한 recursive(int[][] dp, String target, Map<String, Integer> map) 메서드를 수행한 결과를 주어진 문제의 결과로 반환한다.

4. 재귀 호출을 이용하여 순차적으로 모든 문자 조합을 만들 recursive(int[][] dp, String target, Map<String, Integer> map) 메서드를 정의한다.
- map의 target에 해당하는 값이 존재하는 경우, 해당 값을 반환한다.
- 문자 조합에 필요한 변수를 정의한다.
  - min은 최소 문자열 사용 횟수를 저장할 변수로, 정수의 가장 큰 값을 넣어준다.
  - length는 dp의 길이인 stickers의 문자열 갯수를 넣어준다.
  - str은 target의 문자를 넣어줄 변수로, 영문자 갯수은 26의 크기로 초기화 하고 각 위치에 target의 문자 갯수를 기록한다.
- 0부터 length 미만까지 i를 증가하며 아래를 수행한다.
  - target의 첫 문자열로 시작하는 문자열이 아닌 경우, 다음 문자열로 넘어간다.
  - sb는 target을 만들기 위한 문자를 넣을 변수로, StringBuilder로 초기화한다.
  - 0부터 26 미만까지 j를 증가시키며, str[j]와 dp[i][j]의 차이 만큼 sb에 j를 문자로 변환한 값을 넣어준다.
  - temp에 sb를 문자열로 변환한 값을 target 자리에 넣은 재귀 호출 결과를 넣어준다.
  - temp가 -1이 아닌 경우 target을 만들기 위한 문자가 되므로 min과 $temp + 1$ 중 작은 값을 넣어준다.
- map의 target 문자가 키인 값에 min에 값이 들어가면 min을, 아니면 -1을 넣어주고 해당 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/StickersToSpellWord.java){:target="_blank"}에서 확인 가능합니다.