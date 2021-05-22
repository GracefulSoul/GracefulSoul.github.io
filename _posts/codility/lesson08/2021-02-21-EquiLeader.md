---
title: "Codility Java EquiLeader"
excerpt: "Lesson8. Leader"
last_modified_at: 2021-02-21T15:04:00
header:
  image: /assets/images/codility/lesson08/EquiLeader.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Leader
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/8-leader/equi_leader/){:target="_blank"}

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

import java.util.Map;
import java.util.HashMap;
import java.util.Vector;

class Solution {
  public int solution(int[] A) {
    Vector<Integer> record = getRecord(A);
    int result = 0;
    for (int idx = 0; idx < A.length; idx++) {
      int left = record.elementAt(idx);
      int right = record.lastElement() - left;
      int equiOne = ((idx + 1) / 2) + 1;
      int equiTwo = ((A.length - (idx + 1)) / 2) + 1;
      if ((left >= equiOne) && (right >= equiTwo)) {
        result++;
      }
    }
    return result;
  }
  private Vector<Integer> getRecord(int[] A) {
    Vector<Integer> record = new Vector<>();
    int leader = getLeader(A);
    int count = 0;
    for (int num : A) {
      if (num == leader) {
        count++;
      }
      record.add(count);
    }
    return record;
  }
  private int getLeader(int[] A) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int num : A) {
      map.put(num, map.getOrDefault(num, 0) + 1);
    }
    int leader = 0;
    int max = 0;
    for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
      if (entry.getValue() > max) {
        leader = entry.getKey();
        max = entry.getValue();
      }
    }
    return leader;
  }
}
```

# 설명
1. 주어진 배열 A에 들어간 숫자가 몇 번 반복되었는지를 계산하기 위해 Map을 사용한다.
2. 주어진 배열 A를 반복하여 변수 map에 숫자를 key로 반복 횟수를 value로 증가시켜준다.
3. 변수 map에서 가장 많이 반복된 숫자를 가져온다.
4. 리더의 변화를 탐색하기 위해 Vector를 정의하고, 주어진 배열 A를 반복하여 index 별 리더의 수를 계산한다.
5. 계산된 record 기반으로 이분법을 적용하여 동등한 리더의 수를 계산하여 주어진 문제의 결과로 반환한다.
- 좌측의 리더의 수인 변수 left와 우측의 리더의 수인 right를 계산한다.
- 동등한 리더가 되기 위해서는 위치 기반으로 절반 이상의 리더가 존재해야 한다.
- 절반 이사의 리더가 존재하는 경우만 동등한 리더의 수를 계산하는 변수 result를 증가시킨다.

# 결과
[Link](https://app.codility.com/demo/results/trainingT4DHJ8-XJZ/){:target="_blank"}

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson08/EquiLeader.java){:target="_blank"}에서 확인 가능합니다.