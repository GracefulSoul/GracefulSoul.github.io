---
title: "Leetcode Java Number of Flowers in Full Bloom"
excerpt: "Leetcode Hard - 'Number of Flowers in Full Bloom' 문제 Java 풀이"
last_modified_at: 2023-10-11T18:30:00
header:
  image: /assets/images/leetcode/number-of-flowers-in-full-bloom.png
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
[Link](https://leetcode.com/problems/number-of-flowers-in-full-bloom){:target="_blank"}

# 코드
```java
class Solution {

  public int[] fullBloomFlowers(int[][] flowers, int[] people) {
    int length = flowers.length;
    int[] start = new int[length];
    int[] end = new int[length];
    for (int i = 0; i < length; i++) {
      start[i] = flowers[i][0];
      end[i] = flowers[i][1];
    }
    Arrays.sort(start);
    Arrays.sort(end);
    length = people.length;
    int[] result = new int[length];
    for (int i = 0; i < length; i++) {
      result[i] = this.getIndex(start, people[i] + 1) - this.getIndex(end, people[i]);
    }
    return result;
  }

  private int getIndex(int[] flowers, int target) {
    int left = 0;
    int right = flowers.length - 1;
    while (left < right) {
      int mid = left + (right - left) / 2;
      if (flowers[mid] < target) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }
    return flowers[left] >= target ? left : left + 1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-flowers-in-full-bloom/submissions/1072551506/){:target="_blank"}

# 설명
1. people의 위치에 도달할 때 flowers의 개화된 꽃의 갯수를 반환하는 문제이다.
- flowers[i] = [start<sub>i</sub>, end<sub>i</sub>]로, 개화와 낙화의 지점이 저장되어 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 flowers의 길이를 저장한 변수이다.
- start와 end는 flowers의 꽃의 개화 시기와 낙화 시기를 넣을 배열로, 각각 length 크기의 정수 배열로 초기화하여 flowers를 이용하여 꽃의 개화와 낙화 지점를 넣고 오름차순 정렬해준다.
  - start와 end를 오름차순으로 정렬하더라도 각 위치에서 개화된 꽃의 수는 변함이 없다.
- length에 people의 길이를 저장해준다.
- result는 결과를 저장할 변수로, length 길이의 정수 배열로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- result[i] 위치에 4번에서 정의한 getIndex(int[] flowers, int target) 메서드를 start, $people[i] + 1$로 수행한 결과와 end, people[i]로 수행한 결과의 차잇값인 개화된 꽃의 수를 넣어준다.

4. flowers의 target 위치에서 개화된 꽃의 시작과 종료 위치를 탐색하기 위한 getIndex(int[] flowers, int target) 메서드를 정의한다.
- left와 right는 위치 탐색에 필요한 변수로, 0과 $flowers.length - 1$로 초기화한다.
- left가 right 미만일 때 까지 아래를 반복한다.
  - mid에 $left + \frac{right - left}{2}$인 중앙값을 넣어준다.
  - flowers[mid]가 target 미만인 경우, left에 $mid + 1$을 넣어 하한 범위를 높혀준다.
  - 위의 경우가 아니라면, right에 mid를 넣어 상한 범위를 낮혀준다.
- flowers[left]의 값이 target 이상이면 left를 아니면 $left + 1$를 반환한다.

5. 반복이 완료되면 위치 별 개화된 꽃의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfFlowersInFullBloom.java){:target="_blank"}에서 확인 가능합니다.