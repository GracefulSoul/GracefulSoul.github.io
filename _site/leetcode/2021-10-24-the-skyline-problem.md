---
title: "Leetcode Java The Skyline Problem"
excerpt: "Leetcode The Skyline Problem Java 풀이"
last_modified_at: 2021-10-24T13:00:00
header:
  image: /assets/images/leetcode/the-skyline-problem.png
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
[Link](https://leetcode.com/problems/the-skyline-problem/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> getSkyline(int[][] buildings) {
    List<List<Integer>> result = new ArrayList<>();
    Queue<int[]> queue = new PriorityQueue<>((a, b) -> b[2] - a[2]);
    int index = 0;
    int[] building = null;
    while (building != null || index < buildings.length) {
      if (building == null) {
        building = buildings[index];
        this.addPoint(result, building[0], building[2]);
      } else if (index < buildings.length && buildings[index][0] <= building[1]) {
        if (buildings[index][2] > building[2]) {
          if (buildings[index][0] == building[0]) {
            result.remove(result.size() - 1);
          }
          if (buildings[index][1] <= building[1]) {
            queue.add(building);
          }
          building = buildings[index];
          this.addPoint(result, building[0], building[2]);
        } else if (buildings[index][1] > building[1]) {
          queue.add(buildings[index]);
        }
        index++;
      } else {
        int[] lower = queue.poll();
        while (lower != null && lower[1] <= building[1]) {
          lower = queue.poll();
        }
        if (lower == null) {
          this.addPoint(result, building[1], 0);
        } else if (lower[2] < building[2]) {
          this.addPoint(result, building[1], lower[2]);
        }
        building = lower;
      }
    }
    return result;
  }

  private void addPoint(List<List<Integer>> result, int point, int height) {
    List<Integer> temp = new ArrayList<>();
    temp.add(point);
    temp.add(height);
    result.add(temp);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/576219670/){:target="_blank"}

# 설명
1. 주어진 배열인 buildings를 이용하여 x축(point)이 중복되지 않은 y축(height)의 값들을 배열로 넣어 반환하는 문제이다.
- buildings 배열은 [left, right, height]의 세 값이 존재한다.
  - left는 건물의 좌측 가장자리에 해당하는 x축 값이다.
  - right는 건물의 우측 가장자리에 해당하는 x축 값이다.
  - height는 건물의 높이로 y축 값이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 x축(point)이 중복되지 않은 y축(height)의 값들을 넣기 위한 컬렉션이다.
- queue는 building의 값을 저장할 Queue로, 넣은 빌딩의 정보를 높이 순으로 활용하기 위해 [PriorityQueue](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html){:target="_blank"}를 사용한다.
- index는 buildings 배열을 순차적으로 활용하기 위한 인덱스로 0으로 초기화한다.
- building은 buildings 배열의 값을 넣기 위한 변수이다.

3. buiding이 null이 아니거나 index가 buildings.length보다 작을 때 까지 반복하여 모든 result에 중복되지 않은 x축(point)과 y축(height)을 찾아 넣어준다.

4. building이 null인 경우, buildings[index]를 building에 넣어주고 result에 x축과 y축의 정보를 컬렉션으로 넣어준다.

5. index가 buildings.length보다 작아 아직 결과 탐색이 가능하고 buildings[index][0]의 값이 building[1]이 커서 x축이 겹치지 않은 건물이므로 아래를 수행한다.
- buildings[index][2]의 값이 building[2]의 값보다 크면, 기존 건물보다 높은 건물이므로 아래를 수행한다.
  - buildings[index][0]의 값이 building[0]의 값이 동일한 경우, 건물의 시작 위치가 동일하므로 building의 값으로 들어간 result의 마지막 값을 제거해준다.
  - buildings[index][1]의 값이 building[1]의 값보다 작거나 같으면, 건물의 종료 위치가 building이 더 이후이므로 queue에 building을 넣어준다.
  - building에 buildings[index]의 값을 넣어 반복을 계속 수행한다.
- buildings[index][1]의 값이 building[1]의 값보다 크면, building보다 건물의 종료 위치가 더 이후이므로 queue에 buildings[index]를 넣어 반복을 계속 수행한다.
- building의 index번째 값을 사용했으므로, index를 증가시키고 반복을 계속 수행한다.

6. 그 외의 경우, queue의 값을 이용하여 result에 point를 넣어준다.
- lower에 queue에 있는 값을 빼서 넣어준다.
- lower이 null이 아니고 lower[1]의 값이 building[1]의 값보다 작거나 같을 때 까지 queue의 값을 lower에 넣어준다.
- lower이 null인지 검증하여 result에 값을 넣어준다.
  - lower이 null인 경우, result에 building[1]의 값과 0을 이용하여 컬렉션을 만들어 넣어준다.
  - lower이 null이 아닌 경우, building[1]의 값과 lower[2]의 값을 이용하여 컬렉션을 만들어 넣어준다.
- building에 lower 값을 넣어주고 반복을 계속 수행한다.

7. 반복이 완료되면 x축(point)이 중복되지 않은 y축(height)의 값들을 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TheSkylineProblem.java){:target="_blank"}에서 확인 가능합니다.