---
title: "Leetcode Java Letter Tile Possibilities"
excerpt: "Leetcode Letter Tile Possibilities Java"
last_modified_at: 2024-04-13T09:30:00
header:
  image: /assets/images/leetcode/letter-tile-possibilities.png
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
[Link](https://leetcode.com/problems/letter-tile-possibilities/){:target="_blank"}

# 코드
```java
class Solution {

  public int numTilePossibilities(String tiles) {
    int[] count = new int[26];
    for (char c : tiles.toCharArray()) {
      count[c - 'A']++;
    }
    return this.dfs(count);
  }

  private int dfs(int[] count) {
    int sum = 0;
    for (int i = 0; i < 26; i++) {
      if (count[i] > 0) {
        sum++;
        count[i]--;
        sum += this.dfs(count);
        count[i]++;
      }
    }
    return sum;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/letter-tile-possibilities/submissions/1230763585/){:target="_blank"}

# 설명
1. tiles 내 문자들을 이용하여 중복되지 않은 고유 문자열들을 만들 수 있는 최대 갯수를 계산하는 문제이다.

2. count는 tiles내 문자들의 갯수를 계산할 변수로, 영문자 갯수인 26 크기의 정수 배열로 초기화하여 tiles 내 문자들에 해당하는 위치에 갯수를 넣어준다.

3. 4번에서 정의한 dfs(int[] count) 메서드를 수행한 결과를 주어진 문제의 결과로 반환한다.

4. DFS 방식으로 고유 문자열의 갯수를 계산하기 위한 dfs(int[] count) 메서드를 정의한다.
- sum은 고유 문자열 갯수의 합을 저장할 변수로, 0으로 초기화한다.
- 0부터 count의 길이인 26 미만까지 아래를 반복한다.
  - count[i]의 값이 0보다 큰 경우 아래를 수행하고 그 외는 다음 반복을 수행한다.
  - sum을 증가하고 count[i]를 감소시킨다.
  - 감소시킨 count를 이용하여 sum에 재귀호출을 수행한 결과를 더해준다.
  - count[i]를 다시 증가시켜 원복해준다.
- 반복이 완료되어 계산된 고유 문자열의 갯수인 sum을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LetterTilePossibilities.java){:target="_blank"}에서 확인 가능합니다.