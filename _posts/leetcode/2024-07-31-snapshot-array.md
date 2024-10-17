---
title: "Leetcode Java Snapshot Array"
excerpt: "Leetcode Medium - 'Snapshot Array' 문제 Java 풀이"
last_modified_at: 2024-07-31T17:40:00
header:
  image: /assets/images/leetcode/snapshot-array.png
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
[Link](https://leetcode.com/problems/snapshot-array/){:target="_blank"}

# 코드
```java
class SnapshotArray {

  private TreeMap<Integer, Integer>[] snapshotArray;
  private int snapId;

  @SuppressWarnings("unchecked")
  public SnapshotArray(int length) {
    this.snapshotArray = new TreeMap[length];
    for (int i = 0; i < length; i++) {
      this.snapshotArray[i] = new TreeMap<Integer, Integer>();
      this.snapshotArray[i].put(0, 0);
    }
  }

  public void set(int index, int val) {
    this.snapshotArray[index].put(this.snapId, val);
  }

  public int snap() {
    return this.snapId++;
  }

  public int get(int index, int snap_id) {
    return this.snapshotArray[index].floorEntry(snap_id).getValue();
  }

}

/**
 * Your SnapshotArray object will be instantiated and called as such:
 * SnapshotArray obj = new SnapshotArray(length);
 * obj.set(index,val);
 * int param_2 = obj.snap();
 * int param_3 = obj.get(index,snap_id);
 */
```

# 결과
[Link](https://leetcode.com/problems/minimum-deletions-to-make-string-balanced/submissions/1339350919/){:target="_blank"}

# 설명
1. 아래의 기능을 제공하는 SnapshotArray를 완성하는 문제이다.
- 생성자인 SnapshotArray(int length)는 length 크기의 배열을 가진 데이터 구조를 초기화한다.
- 메서드인 set(index, val)은 index번째 요소를 val 값으로 넣어준다.
- 메서드인 snap()은 배열의 스냅샷을 생성하고 생성한 횟수에서 1뺀 값인 snap_id를 반환한다.
- 메서드인 get(index, snap_id)은 index번째 배열의 snap_id에 해당하는 값을 반환한다.

2. SnapshotArray의 기능을 수행하기 위한 전역 변수를 정의한다.
- snapshotArray는 index번째 요소 별 스냅샷을 찍은 결과를 저장할 변수이다.
- snapId는 스냅샷을 찍은 횟수를 저장할 변수이다.

3. 생성자인 SnapshotArray(int length)를 완성한다.
- 전역 변수인 snapshotArray에 length 크기의 TreeMap으로 초기화한다.
- snapshotArray의 모든 값에 TreeMap을 넣고 키와 값이 0인 초기값을 넣어준다.

4. 메서드인 set(index, val)을 완성한다.
- snapshotArray의 index번째 TreeMap에 snapId가 키인 위치에 val을 넣어준다.

5. 메서드인 snap()을 완성한다.
- snapId인 스냅샷을 찍은 횟수를 증가시켜준다.

6. 메서드인 get(index, snap_id)을 완성한다.
- snapshotArray의 index번째 TreeMap에 snap_id와 같거나 작은 값이 키인 값을 가져와 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SnapshotArray.java){:target="_blank"}에서 확인 가능합니다.