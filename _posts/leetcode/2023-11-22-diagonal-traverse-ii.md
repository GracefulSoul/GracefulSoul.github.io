---
title: "Leetcode Java Diagonal Traverse II"
excerpt: "Leetcode Diagonal Traverse II Java"
last_modified_at: 2023-11-22T19:10:00
header:
  image: /assets/images/leetcode/diagonal-traverse-ii.png
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
[Link](https://leetcode.com/problems/diagonal-traverse-ii){:target="_blank"}

# 코드
```java
class Solution {

  public int[] findDiagonalOrder(List<List<Integer>> nums) {
    int max = 0;
    int length = 0;
    List<Integer>[] map = new ArrayList[100001];
    for (int i = 0; i < nums.size(); i++) {
      List<Integer> list = nums.get(i);
      int size = list.size();
      length += size;
      for (int j = 0; j < size; j++) {
        int sum = i + j;
        if (map[sum] == null) {
          map[sum] = new ArrayList<>();
        }
        map[sum].add(list.get(j));
        max = Math.max(max, sum);
      }
    }
    int[] result = new int[length];
    int index = 0;
    for (int i = 0; i <= max; i++) {
      List<Integer> curr = map[i];
      for (int j = curr.size() - 1; j >= 0; j--) {
        result[index++] = curr.get(j);
      }
    }
    return result;
  }


}
```

# 결과
[Link](https://leetcode.com/problems/diagonal-traverse-ii/submissions/1104087099/){:target="_blank"}

# 설명
1. nums 내 값들을 2차원 배열 형태로 구성했을 때, 좌측 상단의 첫 값부터 좌측 아래에서 우측 위로 대각선 방향으로 이동했을 때 만나는 숫자 순서대로 정렬해서 하나의 배열로 만드는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- max는 nums를 이용하여 만들 수 있는 대각선의 갯수로, 0으로 초기화한다.
- length는 nums 내 값들의 수를 저장할 변수로, 0으로 초기화한다.
- map은 대각선대로 값을 이어줄 변수로, 값의 가장 큰 갯수보다 1 큰 100001 크기의 ArrayList 배열로 초기화한다.
  - 위의 값들을 nums를 반복하여 max에 nums의 대각선의 갯수를, length에 nums 내 값들의 수를, map에 $i + j$인 각 대각선 순서대로 첫 행부터 마지막 행까지 값들을 넣어준다.
- result는 숫자들을 순서대로 넣어 줄 배열로, length 길이의 정수 배열로 초기화한다.
- index는 result의 각 위치를 순서대로 넣기 위한 변수로, 첫 위치인 0으로 초기화한다.

3. map을 첫 배열의 List부터 순차적으로 반복하여 역순으로, result에 값을 넣어 주어진 문제의 결과로 반환한다.

# 해설
- 숫자의 대각선 순서대로 저장할 map을 List의 배열로 초기화한 이유는 각 위치는 i번째 행과 j번째 행을 더한 위치가 아래와 같이 순차적으로 계산이 가능하므로 이를 활용한다.
  - 첫 번째 대각선 : $0 + 0 = 0$
  - 두 번째 대각선 : $0 + 1 = 1 + 0 = 1$
  - 세 번쨰 대각선 : $0 + 2 = 1 + 1 = 2 + 0 = 2$
- nums 내 각 List의 값들은 동일하지 않은 길이의 정수 값으로 이루어졌으므로, map에 값이 들어간 List의 수는 map개가 존재하고 result의 길이는 length로 초기화하기 위해 두 값을 계산한다.
- map의 각 List는 첫 행부터 마지막 행 순으로 각 배열에 값을 넣었으므로, 대각선대로 역순으로 result에 값을 넣는다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DiagonalTraverseII.java){:target="_blank"}에서 확인 가능합니다.