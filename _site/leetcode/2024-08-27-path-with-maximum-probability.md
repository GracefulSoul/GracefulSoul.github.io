---
title: "Leetcode Java Path with Maximum Probability"
excerpt: "Leetcode Path with Maximum Probability Java"
last_modified_at: 2024-08-27T18:40:00
header:
  image: /assets/images/leetcode/path-with-maximum-probability.png
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
[Link](https://leetcode.com/problems/path-with-maximum-probability/){:target="_blank"}

# 코드
```java
class Solution {

  public double maxProbability(int n, int[][] edges, double[] succProb, int start_node, int end_node) {
    double[] max = new double[n];
    max[start_node] = 1.0;
    for (int i = 0; i < n - 1; i++) {
      boolean updated = false;
      for (int j = 0; j < edges.length; j++) {
        int a = edges[j][0];
        int b = edges[j][1];
        double probability = succProb[j];
        if (max[a] * probability > max[b]) {
          max[b] = max[a] * probability;
          updated = true;
        }
        if (max[b] * probability > max[a]) {
          max[a] = max[b] * probability;
          updated = true;
        }
      }
      if (!updated) {
        break;
      }
    }
    return max[end_node];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/path-with-maximum-probability/submissions/1369877894/){:target="_blank"}

# 설명
1. n개의 edges와 succProb를 이용하여 start_node에서 end_node까지 갈 수 있는 최대 확률을 반환하는 문제이다.
- edges[i] = [a, b]로, a노드에서 b노드까지 도착할 확률이 succProb[i]를 나타낸다.
- start_node에서 end_node까지 갈 수 없는 경우, 0을 반환한다.

2. max는 도착할 확률이 최대인 값을 구하기 위한 변수로, n 크기의 double형 배열로 정의하고 첫 값을 1.0으로 초기화한다.

3. 0부터 $n - 1$까지 i를 증가시키며 아래를 수행한다.
- updated는 값이 수정되었는지 검증하기 위한 변수로, false로 초기화한다.
- 0부터 edges의 길이 미만까지 j를 증가시키며 아래를 수행한다.
  - a와 b에 edges[j]의 값을 순차적으로 넣어준다.
  - probability에 succProb[j]값인 도착 확률을 넣어준다.
  - $max[a] \times probability$ 값이 max[b]보다 큰 도착 확률이 높은 경우, max[b]에 $max[a] \times probability$ 값을 저장하고 updated를 true를 넣어준다.
  - $max[b] \times probability$ 값이 max[a]보다 큰 도착 확률이 높은 경우, max[a]에 $max[b] \times probability$ 값을 저장하고 updated를 true를 넣어준다.
- updated가 false인 변경되지 않은 경우 더 이상의 최대 확률이 존재하지 않으므로, 반복을 중단한다.

4. 반복이 완료되면 start_node에서 end_node까지 도착할 최대 확률이 저장된 max[end_node]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PathWithMaximumProbability.java){:target="_blank"}에서 확인 가능합니다.