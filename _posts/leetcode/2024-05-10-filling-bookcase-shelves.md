---
title: "Leetcode Java Filling Bookcase Shelves"
excerpt: "Leetcode Filling Bookcase Shelves Java"
last_modified_at: 2024-05-10T11:40:00
header:
  image: /assets/images/leetcode/filling-bookcase-shelves.png
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
[Link](https://leetcode.com/problems/filling-bookcase-shelves/){:target="_blank"}

# 코드
```java
class Solution {

  public int minHeightShelves(int[][] books, int shelfWidth) {
    int length = books.length;
    int[] dp = new int[length + 1];
    for (int i = 1; i <= length; i++) {
      int width = books[i - 1][0];
      int height = books[i - 1][1];
      dp[i] = dp[i - 1] + height;
      for (int j = i - 1; j > 0 && width + books[j - 1][0] <= shelfWidth; j--) {
        height = Math.max(height, books[j - 1][1]);
        width += books[j - 1][0];
        dp[i] = Math.min(dp[i], dp[j - 1] + height);
      }
    }
    return dp[length];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/filling-bookcase-shelves/submissions/1254051490/){:target="_blank"}

# 설명
1. books를 이용하여 shelfWidth 너비의 선반에 책을 순서대로 배치할 때, 책장의 가능한 최소 높이를 반환하는 문제이다.
- books[i] = [thickness<sub>i</sub>, high<sub>i</sub>]로, 두께와 높이 정보를 담고 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 books의 길이인 책의 갯수를 저장한 변수이다.
- dp는 최소 높이를 계산하기 위해 사용할 배열로, $length + 1$크기의 정수 배열로 초기화한다.

3. 1부터 length 이하까지 i를 증가시키며 아래를 반복한다.
- width와 height에 books[$i - 1$]의 두께와 높이 값을 넣어준다.
- dp[i]에 이전 값인 dp[$i - 1$]의 값에 height를 더해준다.
- $i - 1$부터 0 초과일 때 까지 j를 감소시키고 $width + books[j - 1][0]$의 값이 shelfWidth 이하인 선반 너비를 초과하지 않을 때 까지 아래를 반복한다.
  - heigh에 현재 책의 높이인 heigh와 books의 $j - 1$번째 책의 높이 중 큰 값을 넣어준다.
  - width에 books의 $j - 1$번째 책의 두께를 넣어준다.
  - dp[i]에 현재까지 최소 높이인 dp[i]와 $dp[j - 1] + height$ 값인 $j - 1$번째 책이 있는 선반에 책을 같이 배치할 경우에 대한 높이 중 작은 값을 넣어준다.

4. 반복이 완료되면 최소 높이가 저장된 dp[length]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FillingBookcaseShelves.java){:target="_blank"}에서 확인 가능합니다.