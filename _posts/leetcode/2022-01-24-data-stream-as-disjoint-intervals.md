---
title: "Leetcode Java Data Stream as Disjoint Intervals"
excerpt: "Leetcode - 'Data Stream as Disjoint Intervals' 문제 Java 풀이"
last_modified_at: 2022-01-24T17:00:00
header:
  image: /assets/images/leetcode/data-stream-as-disjoint-intervals.png
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
[Link](https://leetcode.com/problems/data-stream-as-disjoint-intervals/){:target="_blank"}

# 코드
```java
class SummaryRanges {

  private List<int[]> list;

  public SummaryRanges() {
    this.list = new ArrayList<>();
  }

  public void addNum(int val) {
    int idx = this.binarySearch(val);
    if (idx >= 0 && val >= this.list.get(idx)[0] && val <= this.list.get(idx)[1]) {
      return;
    }
    int[] cur = new int[] { val, val };
    if (idx >= 0) {
      int[] pre = this.list.get(idx);
      if (pre[1] + 1 == val) {
        this.list.remove(idx);
        cur[0] = pre[0];
        idx--;
      }
    }
    if (idx + 1 < this.list.size()) {
      int[] next = this.list.get(idx + 1);
      if (val + 1 == next[0]) {
        this.list.remove(idx + 1);
        cur[1] = next[1];
      }
    }
    this.list.add(idx + 1, cur);
  }

  public int[][] getIntervals() {
    int size = this.list.size();
    int[][] intervals = new int[size][];
    for (int idx = 0; idx < size; idx++) {
      intervals[idx] = this.list.get(idx);
    }
    return intervals;
  }

  private int binarySearch(int num) {
    int left = 0;
    int right = this.list.size() - 1;
    while (left <= right) {
      int mid = left + (right - left) / 2;
      if (num < this.list.get(mid)[0]) {
        right = mid - 1;
      } else if (num > list.get(mid)[0]) {
        left = mid + 1;
      } else {
        return mid;
      }
    }
    return right;
  }

}

/**
 * Your SummaryRanges object will be instantiated and called as such:
 * SummaryRanges obj = new SummaryRanges();
 * obj.addNum(val);
 * int[][] param_2 = obj.getIntervals();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/626638928/){:target="_blank"}

# 설명
1. 숫자를 추가하면 기존 숫자들을 이용하여 연속된 숫자들의 부분 범위를 지정하여 데이터 스트림으로 보관하는 SummaryRanges 클래스를 완성하는 문제이다.
- 생성자인 SummaryRanges()는 빈 스트림 객체를 초기화 하는 역할을 수행한다.
- 메서드인 addNum(int val)은 연속된 숫자들의 부분 범위를 지정하기 위한 정수인 val를 주입하는 역할을 수행한다.
- 메서드인 getIntervals()는 연속된 숫자들의 부분 범위를 저장한 데이터 스트림을 반환하는 역할을 수행한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- list는 연속된 숫자들의 부분 범위를 저장한 데이터 스트림을 임시 보관할 변수이다.

3. 생성자인 SummaryRanges()를 완성한다.
- 전역 변수인 list를 새 ArrayList를 생성하여 초기화 시켜준다.

4. addNum(int val) 메서드를 통해 주입된 val의 값을 넣기 위한 위치를 탐색하기 위한 binarySearch(int num) 메서드를 완성한다.
- 좌측에서 탐색하기 위한 변수인 left를 0으로, 우측에서 탐색하기 위한 변수인 right를 $list.size() - 1$로 초기화 한다.
- left가 right보다 작거나 같을 때 까지 반복하여 위치 탐색을 수행한다.
  - mid에 $left + \frac{right - left}{2}$의 결과를 넣어준다.
  - list의 mid번째 배열의 첫 값이 num보다 클 경우, right에 $mid - 1$을 넣어 탐색 범위를 좁혀준다.
  - list의 mid번째 배열의 첫 값이 num보다 작을 경우, left에 $mid + 1$을 넣어 탐색 범위를 좁혀준다.
  - 그 외인 두 값이 같은 경우, mid를 반환한다.
- 반복이 완료되면 최대한 좁혀진 right의 값을 위치 값으로 반환한다.

5. 메서드인 addNum(int val)을 완성한다.
- idx에 4번에서 정의한 binarySearch() 메서드를 활용하여 구해진 위치 값을 넣어준다.
- idx가 0보다 크고, val의 값이 list의 idx번째 배열의 첫 값보다 크고 두번째 값보다 작거나 같은 경우 해당 영역에 포함되는 값이므로 그만 수행한다.
- 현재 값을 임시 부분 배열로 cur 배열을 선언하고 val 값을 첫 번째와 두 번째 위치에 넣어준다.
- idx가 0보다 큰 경우 아래를 수행한다.
  - pre에 list의 idx번째 배열을 넣어준다.
  - pre의 두 번째 값에 1을 더한 값이 val 값과 동일한 경우 해당 부분 영역의 길이에 val 값을 합칠 수 있으므로, list에서 idx번째 객체를 삭제하고 cur의 첫 값에 pre의 첫 값을 넣어 idx를 감소시킨다.
- $idx + 1$이 list의 크기보다 작은 경우 아래를 수행한다.
  - next에 list의 $idx + 1$번째 배열을 넣어준다.
  - $val + 1$이 next의 첫 번째 값과 동일한 경우 next의 값이 조금 더 크므로, list에서 $idx + 1$번째 값을 제거하고 cur의 두 번째 값에 next의 두 번째 값을 넣어준다.
- 위의 모든 과정이 완료되면 list의 $idx + 1$번째 위치에 cur 배열을 넣어주어 데이터 스트림을 만들어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DataStreamAsDisjointIntervals.java){:target="_blank"}에서 확인 가능합니다.