---
title: "Leetcode Java Restore the Array From Adjacent Pairs"
excerpt: "Leetcode Medium - 'Restore the Array From Adjacent Pairs' 문제 Java 풀이"
last_modified_at: 2023-11-10T19:00:00
header:
  image: /assets/images/leetcode/restore-the-array-from-adjacent-pairs.png
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
[Link](https://leetcode.com/problems/restore-the-array-from-adjacent-pairs){:target="_blank"}

# 코드
```java
class Solution {

  public int[] restoreArray(int[][] adjacentPairs) {
    int length = adjacentPairs.length;
    Map<Integer, int[]> map = new HashMap<>();
    for (int i = 0; i < length; i++) {
      int[] adjacentPair = adjacentPairs[i];
      if (map.containsKey(adjacentPair[0])) {
        map.get(adjacentPair[0])[1] = adjacentPair[1];
      } else {
        map.put(adjacentPair[0], new int[] { adjacentPair[1], -1000000 });
      }
      if (map.containsKey(adjacentPair[1])) {
        map.get(adjacentPair[1])[1] = adjacentPair[0];
      } else {
        map.put(adjacentPair[1], new int[] { adjacentPair[0], -1000000 });
      }
    }
    int[] result = new int[length + 1];
    int start = -1000000;
    for (Map.Entry<Integer, int[]> entry : map.entrySet()) {
      if (entry.getValue()[1] == -1000000) {
        start = entry.getKey();
        break;
      }
    }
    result[0] = start;
    for (int i = 1, value = -1000000; i < result.length; i++) {
      int[] pair = map.get(start);
      int temp = pair[0] == value ? pair[1] : pair[0];
      result[i] = temp;
      value = start;
      start = temp;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/restore-the-array-from-adjacent-pairs/submissions/1095856737/){:target="_blank"}

# 설명
1. 아래의 조건을 만족하는 adjacentPairs를 이용하여 인접한 값끼리 묶어서 하나의 배열로 반환하는 문제이다.
- adjacentPairs[i] = [u<sub>i</sub>, v<sub>i</sub>]는 u<sub>i</sub>와 v<sub>i</sub>가 인접하다는 의미이다.
- 순서에 상관 없이, 조건을 만족하는 배열을 만들어 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 adjacentPairs의 길이를 저장한 변수이다.
- map은 adjacentPairs의 임의 값에 대한 연관된 값들을 모아 저장할 변수로, HashMap으로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키면서 아래를 수행한다.
- adjacentPair에 adjacentPairs의 i번째 배열을 넣어준다.
- map에 adjacentPair[0]의 값이 map 내 키로 존재하는지에 따라 아래를 수행한다.
  - 존재하는 경우, 해당 키의 값인 배열에 adjacentPair[1]의 값을 넣어준다.
  - 존재하지 않는 경우, 해당 키에 연관된 adjacentPair[1]의 값과 값 범위의 하한값인 -100000을 배열로 넣어준다.
- map에 adjacentPair[1]의 값이 map 내 키로 존재하는지에 따라 아래를 수행한다.
  - 존재하는 경우, 해당 키의 값인 배열에 adjacentPair[0]의 값을 넣어준다.
  - 존재하지 않는 경우, 해당 키에 연관된 adjacentPair[0]의 값과 값 범위의 하한값인 -100000을 배열로 넣어준다.

4. start는 시작 값을 찾기 위한 변수로 값의 하한 값인 -100000으로, result는 결과를 넣을 배열로 $length + 1$ 크기의 정수 배열로 초기화한다.

5. map을 순환하면서 값인 배열의 두 번째 값이 -100000인 연관된 값이 하나만 존재하는 경우, start에 해당 key 값을 넣고 반복을 종료한다.
- 순서는 상관 없으므로, 시작 값이든 종료 값이든 상관이 없다.

6. 시작 값인 result[0] 값에 start를 넣어준다.

7. value는 값의 하한 값인 -10000으로 정의하고, 1부터 result의 길이 미만까지 i를 증가시키면서 아래를 반복한다.
- pair에 map의 start번째 값을 꺼내 넣어준다.
- temp에 pair의 첫 값이 value와 같으면 두 번째 값을, 아니면 첫 번째 값을 넣어준다.
- result[i]에 temp를, value에 start를, start에 temp를 순차적으로 넣어준다.

8. 반복이 완료되면 연관된 값들을 모아 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RestoreTheArrayFromAdjacentPairs.java){:target="_blank"}에서 확인 가능합니다.