---
title: "Leetcode Java Flood Fill"
excerpt: "Leetcode - 'Flood Fill' 문제 Java 풀이"
last_modified_at: 2022-11-23T19:20:00
header:
  image: /assets/images/leetcode/flood-fill.png
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
[Link](https://leetcode.com/problems/flood-fill){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] floodFill(int[][] image, int sr, int sc, int color) {
    if (image[sr][sc] != color) {
      this.dfs(image, sr, sc, image[sr][sc], color);
    }
    return image;
  }

  private void dfs(int[][] image, int sr, int sc, int color, int newColor) {
    if (sr >= 0 && sr < image.length && sc >= 0 && sc < image[0].length && image[sr][sc] == color) {
      image[sr][sc] = newColor;
      this.dfs(image, sr + 1, sc, color, newColor);
      this.dfs(image, sr - 1, sc, color, newColor);
      this.dfs(image, sr, sc + 1, color, newColor);
      this.dfs(image, sr, sc - 1, color, newColor);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/848535900/){:target="_blank"}

# 설명
1. image[sr][sc]에서 시작하여 4 방향의 색상이 동일한 경우, color를 넣어 수정된 image를 반환하는 문제이다.

2. image[sr][sc]의 생상이 color와 동일하지 않은 경우만 3번에서 정의한 dfs(int[][] image, int sr, int sc, int color, int newColor) 메서드를 수행한다.
- 시작 지점의 색상인 image[sr][sc]가 color와 동일하면 예시에서 제공한대로 이미지를 변경하지 않는다.

3. DFS 방식으로 color를 채워 넣을 dfs(int[][] image, int sr, int sc, int color, int newColor) 메서드를 정의한다.
- sr이 [0, image.length]를 만족하고, sc도 image[0].length를 만족하면서 image[sr][sc]의 색상이 동일한 경우, 상하좌우에 대한 재귀 호출을 수행한다.

4. 반복이 완료되면 주어진 조건에 맞춘 color를 image에 채워넣어 수정된 image를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FloodFill.java){:target="_blank"}에서 확인 가능합니다.