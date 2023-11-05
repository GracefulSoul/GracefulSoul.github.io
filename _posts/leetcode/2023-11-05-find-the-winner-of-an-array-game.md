---
title: "Leetcode Java Find the Winner of an Array Game"
excerpt: "Leetcode Find the Winner of an Array Game Java"
last_modified_at: 2023-11-05T17:00:00
header:
  image: /assets/images/leetcode/find-the-winner-of-an-array-game.png
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
[Link](https://leetcode.com/problems/find-the-winner-of-an-array-game){:target="_blank"}

# 코드
```java
class Solution {

  public int getWinner(int[] arr, int k) {
    int result = arr[0];
    int count = 0;
    for (int i = 1; i < arr.length; i++) {
      if (result < arr[i]) {
        result = arr[i];
        count = 0;
      }
      if (++count == k) {
        break;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-winner-of-an-array-game/submissions/1091875432/){:target="_blank"}

# 설명
1. 모두 다른 값으로 구성된 정수 배열인 arr 내 값들 중 아래의 규칙대로 k번 승리한 값을 반환하는 문제이다.
- 최초 승리자는 arr의 맨 앞의 값으로, 1번 승리한 값으로 시작한다.
- arr의 맨 앞의 값이 다음번째 값보다 큰 경우 승리한다.
- 패배한 값은 배열의 맨 마지막으로 이동한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 현재 승리한 값을 저장할 변수로, 첫 승리자인 arr[0]의 값을 넣어준다.
- count는 현재까지 승리한 횟수를 저장할 변수로, 0으로 초기화한다.

3. 1부터 arr 길이 미만까지 i를 증가시키며 아래를 반복한다.
- result가 arr[i]의 값보다 작은 경우, 패배하였으므로 result에 arr[i]의 값을 넣고 count를 0으로 초기화한다.
- 이긴 횟수인 count를 증가시킨 후 count가 k와 동일한 경우, 반복을 종료한다.

4. 위의 반복에서 찾은 k번 이긴 숫자인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindTheWinnerOfAnArrayGame.java){:target="_blank"}에서 확인 가능합니다.