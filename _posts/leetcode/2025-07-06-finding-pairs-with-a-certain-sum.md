---
title: "Leetcode Java Finding Pairs With a Certain Sum"
excerpt: "Leetcode - 'Finding Pairs With a Certain Sum' 문제 Java 풀이"
last_modified_at: 2025-07-06T11:30:00
header:
  image: /assets/images/leetcode/finding-pairs-with-a-certain-sum.png
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
[Link](https://leetcode.com/problems/finding-pairs-with-a-certain-sum/){:target="_blank"}

# 코드
```java
class FindSumPairs {

  private int[] nums1;
  private int[] nums2;
  private Map<Integer, Integer> map;

  public FindSumPairs(int[] nums1, int[] nums2) {
    this.nums1 = nums1;
    this.nums2 = nums2;
    this.map = new HashMap<>();
    for (int num : nums2) {
      this.increase(num, 1);
    }
  }

  public void add(int index, int val) {
    this.increase(this.nums2[index], -1);
    this.nums2[index] += val;
    this.increase(this.nums2[index], 1);
  }

  public int count(int tot) {
    int result = 0;
    for (int num : nums1) {
      result += this.map.getOrDefault(tot - num, 0);
    }
    return result;
  }

  private void increase(int key, int value) {
    this.map.put(key, this.map.getOrDefault(key, 0) + value);
  }

}

/**
 * Your FindSumPairs object will be instantiated and called as such:
 * FindSumPairs obj = new FindSumPairs(nums1, nums2);
 * obj.add(index,val);
 * int param_2 = obj.count(tot);
 */
```

# 결과
[Link](https://leetcode.com/problems/finding-pairs-with-a-certain-sum/submissions/1687799416/){:target="_blank"}

# 설명
1. 아래의 기능을 수행하는 FindSumPairs 객체를 완성하는 문제이다.
- 생성자인 FindSumPairs(int[] nums1, int[] nums2)는 nums1과 nums2를 이용하여 객체를 초기화한다.
- 메서드인 add(int index, int val)는 nums2[index]의 위치에 val 값을 더해준다.
- 메서드인 count(int tot)는 $nums1[i] + nums2[j] == tot$를 만족하는 조합의 갯수를 반환한다.

2. 기능 수행에 필요한 전역 변수를 정의한다.
- nums1과 nums2는 생성자를 통해 주어지는 정수 배열을 저장할 변수이다.
- map은 합계의 갯수를 저장할 변수이다.

3. 생성자인 FindSumPairs(int[] nums1, int[] nums2)를 완성한다.
- nums1과 nums2에 주어진 배열을 넣어 초기화한다.
- map은 HashMap으로 초기화 후, nums2의 각 값을 순차적으로 num에 넣어 map의 num에 해당하는 위치의 값을 1 증가시킨다.

4. 메서드인 add(int index, int val)를 완성한다.
- 이전 값인 map 내 nums2[index]에 해당하는 값을 1 감소시킨다.
- nums2[index] 값에 val을 더해준다.
- 변경된 값인 map 내 nums2[index]에 해당하는 값을 1 증가시킨다.

5. 메서드인 count(int tot)를 완성한다.
- result는 갯수를 계산하기 위한 변수로, 0으로 초기화한다.
- nums1을 순차적으로 num에 넣어 result에 $tot - num$에 해당하는 위치 값을 더해준다.
- 계산된 조건을 만족하는 값의 갯수인 result를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindingPairsWithACertainSum.java){:target="_blank"}에서 확인 가능합니다.