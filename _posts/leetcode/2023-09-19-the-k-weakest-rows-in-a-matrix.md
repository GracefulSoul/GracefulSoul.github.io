---
title: "Leetcode Java The K Weakest Rows in a Matrix"
excerpt: "Leetcode The K Weakest Rows in a Matrix Java"
last_modified_at: 2023-09-19T18:40:00
header:
  image: /assets/images/leetcode/the-k-weakest-rows-in-a-matrix.png
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
[Link](https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix){:target="_blank"}

# 코드
```java
class Solution {

  public int[] kWeakestRows(int[][] mat, int k) {
    Queue<int[]> queue = new PriorityQueue<>((a, b) -> a[0] != b[0] ? b[0] - a[0] : b[1] - a[1]);
    int[] result = new int[k];
    for (int i = 0; i < mat.length; i++) {
      queue.offer(new int[] { this.find(mat[i]), i });
      if (queue.size() > k) {
        queue.poll();
      }
    }
    while (k > 0) {
      result[--k] = queue.poll()[1];
    }
    return result;
  }

  private int find(int[] row) {
    int low = 0;
    int high = row.length;
    while (low < high) {
      int mid = low + (high - low) / 2;
      if (row[mid] == 1) {
        low = mid + 1;
      } else {
        high = mid;
      }
    }
    return low;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/submissions/1053417948/){:target="_blank"}

# 설명
1. 아래의 규칙을 만족하는 이진 정수 배열인 mat 내 약한 순서대로 k개의 행 위치 값을 반환하는 문제이다.
- mat내 값은 0(민간인), 1(군인)으로 구성되며 군인은 민간인 앞에 위치한다.
- 아래 중 하나를 만족하는 경우, i가 j보다 약하다.
  - i열의 군인의 수가 j열의 군인의 수보다 작다.
  - i열과 j열의 군인의 수가 같으면서, i < j 를 만족한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- queue는 크기 순으로 행과 군인의 수를 저장할 변수로, 군인의 수가 같지 않으면 행의 위치 차이로 아니면 군인 수의 차이로 내림차순 정렬하여 저장할 수 있도록 초기화한다.
- result는 결과를 저장할 변수로, k 크기의 정수 배열로 초기화한다.

3. 0부터 mat의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- queue에 4번에서 정의한 find(int[] row) 메서드를 mat[i]로 수행한 결과와 i를 배열로 넣어준다.
- queue의 크기가 k보다 큰 경우, 가장 큰 값인 앞의 값을 꺼내서 queue에서 제거한다.

4. 군인의 수를 탐색하기 위한 find(int[] row) 메서드를 정의한다.
- low와 high는 마지막 군인의 위치를 탐색할 변수로, 0과 row의 길이로 초기화한다.
- low가 high보다 작을 때 까지 아래를 반복한다.
  - mid에 $low + \frac{high - low}{2}$인 중앙값을 넣어준다.
  - row[mid]가 1(군인)인 경우, low에 $mid + 1$을 넣고 아니면 high에 mid를 넣어준다.
- 반복이 완료되면 마지막 군인의 위치인 low를 반환한다.

5. k가 0 이상일 때 까지 k를 감소시키며 result의 역순으로 queue의 값을 꺼내 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TheKWeakestRowsInAMatrix.java){:target="_blank"}에서 확인 가능합니다.