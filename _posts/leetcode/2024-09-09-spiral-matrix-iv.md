---
title: "Leetcode Java Spiral Matrix IV"
excerpt: "Leetcode Medium - 'Spiral Matrix IV' 문제 Java 풀이"
last_modified_at: 2024-09-09T21:10:00
header:
  image: /assets/images/leetcode/spiral-matrix-iv.png
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
[Link](https://leetcode.com/problems/spiral-matrix-iv/){:target="_blank"}

# 코드
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {

  public int[][] spiralMatrix(int m, int n, ListNode head) {
    int[][] result = new int[m][n];
    for (int[] row : result) {
      Arrays.fill(row, -1);
    }
    int top = 0;
    int bottom = m - 1;
    int left = 0;
    int right = n - 1;
    while (head != null) {
      for (int col = left; col <= right && head != null; col++) {
        result[top][col] = head.val;
        head = head.next;
      }
      top++;
      for (int row = top; row <= bottom && head != null; row++) {
        result[row][right] = head.val;
        head = head.next;
      }
      right--;
      for (int col = right; col >= left && head != null; col--) {
        result[bottom][col] = head.val;
        head = head.next;
      }
      bottom--;
      for (int row = bottom; row >= top && head != null; row--) {
        result[row][left] = head.val;
        head = head.next;
      }
      left++;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/spiral-matrix-iv/submissions/1384195866/){:target="_blank"}

# 설명
1. head의 값들을 $m \times n$ 크기의 배열을 만들어 나선형으로 이동하면서 값을 넣어주는 문제이다.
- 값을 채운 나머지 위치에는 -1을 넣어준다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과를 넣을 변수로, $m \times n$ 크기의 2차원 정수 배열로 초기화하고 모든 위치에 -1을 넣어준다.
- top, bottom, left, right는 각각 result의 각 위치를 저장할 변수로, 0, $m - 1$, 0, $n - 1$로 초기화한다.

3. head가 null이 아닐 때 까지 아래를 반복한다.
- result의 top번째 행의 좌측에서 우측으로 head의 값을 꺼내 넣어준 후, top을 증가시켜 아래 줄로 이동한다.
- result의 right번째 열의 위에서 아래로 head의 값을 꺼내 넣어준 후, right를 감소하여 왼쪽 열로 이동한다.
- result의 bottom번째 행의 우측에서 좌측으로 head의 값을 꺼내 넣어준 후, bottom을 감소시켜 윗 줄로 이동한다.
- result의 left번째 열의 아래에서 위로 head의 값을 꺼내 넣어준 후, left를 증가시켜 오른쪽 열로 이동한다.

4. 3번의 반복이 완료되어 head의 값이 순차적으로 입력된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SpiralMatrixIV.java){:target="_blank"}에서 확인 가능합니다.