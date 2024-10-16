---
title: "Leetcode Java Flipping an Image"
excerpt: "Leetcode Flipping an Image Java"
last_modified_at: 2023-02-07T19:30:00
header:
  image: /assets/images/leetcode/flipping-an-image.png
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
[Link](https://leetcode.com/problems/flipping-an-image){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] flipAndInvertImage(int[][] image) {
    for (int[] row : image) {
      for (int left = 0, right = row.length - 1; left <= right;) {
        int temp = row[left];
        row[left++] = 1 - row[right];
        row[right--] = 1 - temp;
      }
    }
    return image;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/positions-of-large-groups/submissions/893261283/){:target="_blank"}

# 설명
1. $n \times n$의 2차원 배열인 image를 수평으로 뒤집은 후 값을 반전시킨 결과를 반환하는 문제이다.
- 수평으로 뒤집는다는 의미는 임의 행인 [0, 1, 1]의 중간 위치를 기준으로 좌우의 값을 바꾸어 [1, 1, 0]이 된다는 의미이다.
- 값을 반전시킨다는 의미는 위의 [1, 1, 0]을 [0, 0, 1]로 1과 0을 바꾸어 준다는 의미이다.

2. image의 각 행을 row에 넣은 후 아래를 반복한다.
- left는 0, right는 $row.length - 1$로 right가 left보다 크거나 같을 때 까지 아래를 반복한다.
  - temp에 row의 left 값을 임시 보관하고 1에서 row의 right번째 값을 뺀 값을 해당 위치에 넣고 left를 증가시킨다.
  - row의 right의 위치에 1에서 temp를 뺀 값을 넣고 right를 감소시킨다.

3. 반복이 완료되면 결과가 저장된 image를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FlippingAnImage.java){:target="_blank"}에서 확인 가능합니다.