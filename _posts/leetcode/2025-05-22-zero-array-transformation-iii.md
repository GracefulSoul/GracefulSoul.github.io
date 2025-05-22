---
title: "Leetcode Java Zero Array Transformation III"
excerpt: "Leetcode - 'Zero Array Transformation III' 문제 Java 풀이"
last_modified_at: 2025-05-22T19:00:00
header:
  image: /assets/images/leetcode/zero-array-transformation-iii.png
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
[Link](https://leetcode.com/problems/zero-array-transformation-iii/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxRemoval(int[] nums, int[][] queries) {
    int length = nums.length;
    int queryCount = queries.length;
    Arrays.sort(queries, (a, b) -> a[0] - b[0]);
    Queue<Integer> queue = new PriorityQueue<>();
    int[] end = new int[length + 1];
    int j = 0;
    int curr = 0;
    for (int i = 0; i < length; i++) {
      curr -= end[i];
      while (j < queryCount && queries[j][0] <= i) {
        queue.offer(-queries[j++][1]);
      }
      while (curr < nums[i]) {
        if (queue.isEmpty() || -queue.peek() < i) {
          return -1;
        }
        end[-queue.poll() + 1]++;
        curr++;
      }
    }
    return queue.size();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/zero-array-transformation-iii/submissions/1641174043/){:target="_blank"}

# 설명
1. nums 내 각 값들을 아래 규칙대로 값을 제거할 때, 모든 값을 0으로 변환 가능한 쿼리를 남기고 제거할 쿼리의 갯수를 계산하는 문제이다.
- queries[i] = [l<sub>i</sub>, r<sub>i</sub>]로, nums의 [l<sub>i</sub>, r<sub>i</sub>] 범위 내 값들 중 선택하여 최대 1씩 감소시킬 수 있다.
- 만일 모든 값을 0으로 변환할 수 없는 경우, -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의하고 값을 정렬한다.
- length와 queryCount는 nums와 queries의 길이를 각각 저장한 변수이다.
- queries의 각 값을 시작 위치부터 오름차순 정렬해준다.
- queue는 사용할 쿼리의 종료 위치를 저장할 변수로, 종료 위치를 오름차순 정렬된 값을 저장하기 위해 PriorityQueue로 초기화한다.
- end는 위치 별 사용할 쿼리의 갯수를 계산할 변수로, $length + 1$ 크기의 정수 배열로 초기화한다.
- j는 queries를 탐색할 위치 변수로, 0으로 초기화한다.
- curr은 현재 사용할 쿼리의 갯수를 계산할 변수로, 0으로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- curr에 end[i]의 현재 위치에 사용 쿼리 갯수를 빼준다.
- j가 queryCount 미만이면서 queries[j][0]의 값이 i 이하인 이전 위치의 값까지, queue에 queries[j][1]의 값을 음수로 넣고 j를 증가시켜준다.
- curr이 nums[i]의 값보다 작을 때 까지 아래를 반복한다.
  - queue가 비어있거나 queue의 맨 앞의 값을 양수로 변환한 값이 i 미만인 현재 위치의 값을 0으로 변경할 수 없는 경우, -1을 주어진 문제의 결과로 반환한다.
  - end의 queue의 맨 앞의 값을 양수로 변환한 값에 1 증가시킨 위치의 값과 curr의 값을 증가시켜준다.

4. 반복이 완료되면 모든 값을 0으로 변환하고 남은 쿼리의 갯수인 queue의 크기를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ZeroArrayTransformationIII.java){:target="_blank"}에서 확인 가능합니다.