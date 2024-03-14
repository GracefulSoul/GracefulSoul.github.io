---
title: "Leetcode Java Flower Planting With No Adjacent"
excerpt: "Leetcode Flower Planting With No Adjacent Java"
last_modified_at: 2024-03-14T19:40:00
header:
  image: /assets/images/leetcode/flower-planting-with-no-adjacent.png
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
[Link](https://leetcode.com/problems/flower-planting-with-no-adjacent){:target="_blank"}

# 코드
```java
class Solution {

  public int[] gardenNoAdj(int n, int[][] paths) {
    List<Integer>[] graph = new ArrayList[n];
    for (int i = 0; i < n; i++) {
      graph[i] = new ArrayList<>();
    }
    for (int[] path : paths) {
      int x = path[0] - 1;
      int y = path[1] - 1;
      graph[x].add(y);
      graph[y].add(x);
    }
    int[] result = new int[n];
    for (int i = 0; i < n; i++) {
      int[] colors = new int[5];
      for (int neighbor : graph[i]) {
        colors[result[neighbor]] = 1;
      }
      for (int j = 4; j > 0; j--) {
        if (colors[j] == 0) {
          result[i] = j;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/flower-planting-with-no-adjacent/submissions/1203375801/){:target="_blank"}

# 설명
1. 1 ~ n까지의 정원을 아래의 규칙대로 1 ~ 4의 색을 가진 꽃들을 심을 경우, 정원 별 심은 꽃을 정수 배열로 순차적으로 넣어 반환하는 문제이다.
- paths[i] = [x<sub>i</sub>, y<sub>i</sub>]는 x<sub>i</sub>번째 정원에서 y<sub>i</sub>번째 정원으로 이동하는 경로가 저장되어 있다.
- 정원은 최대 3개의 길로 왕래가 가능하며, 연결된 정원은 서로 다른 꽃이 심어져야 한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- graph는 1 ~ n까지의 정원의 연결된 경로를 저장할 변수로, 각 위치에 ArrayList로 초기화 후 paths를 반복하여 graph의 $path[0] - 1$번째 ArrayList에 $path[1] - 1$을, $path[1] - 1$번째 ArrayList에 $path[0] - 1$를 넣어준다.
- result는 결과를 저장할 변수로, n 크기의 정수 배열로 초기화한다.

3. 0부터 n까지 i를 증가시키며 아래를 반복한다.
- colors는 i번째 정원과 연결된 꽃의 색상을 저장할 배열로, 값을 체크하기 쉽도록 5 크기의 정수 배열로 초기화 후 graph의 i번째 ArrayList를 반복하여 연결된 정원 내 꽃의 색상에 대한 번호에 1을 넣어준다.
- 4부터 0 초과일 때 까지 j를 감소시키며 아래를 수행한다.
  - colors[j]가 0인 연결된 정원들 내 존재하지 않는 꽃의 색인 경우, result[i]의 위치에 j를 넣어준다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FlowerPlantingWithNoAdjacent.java){:target="_blank"}에서 확인 가능합니다.