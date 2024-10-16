---
title: "Leetcode Java Top K Frequent Elements"
excerpt: "Leetcode Top K Frequent Elements Java 풀이"
last_modified_at: 2022-01-21T21:00:00
header:
  image: /assets/images/leetcode/top-k-frequent-elements.png
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
[Link](https://leetcode.com/problems/top-k-frequent-elements/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] topKFrequent(int[] nums, int k) {
    int min = nums[0];
    int max = nums[0];
    for (int num : nums) {
      if (num < min) {
        min = num;
      } else if (num > max) {
        max = num;
      }
    }
    Num[] array = new Num[max - min + 1];
    for (int num : nums) {
      if (array[num - min] == null) {
        array[num - min] = new Num(num);
      } else {
        array[num - min].count++;
      }
    }
    Arrays.sort(array, new Comparator<Num>() {
      @Override
      public int compare(Num o1, Num o2) {
        if (o1 == null) {
          return 1;
        } else if (o2 == null) {
          return -1;
        } else {
          return o2.count - o1.count;
        }
      }
    });
    int[] result = new int[k];
    for (int i = 0; i < k; i++) {
      result[i] = array[i].value;
    }
    return result;
  }

}

class Num {

  public int value;
  public int count;

  public Num(int value) {
    this.value = value;
    this.count = 1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/624595612/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums의 k번쨰 가장 많이 발생한 값들을 반환하는 문제이다.

2. min과 max에 nums의 첫 값을 넣어주고, nums를 순회하면서 최소값과 최대값을 각 변수에 넣어준다.

3. Num을 이용해 배열의 크기를 최소화 하기 위해 $max - min + 1$ 크기로 정의한다.
- Num은 특정 값인 value의 발생 빈도인 count를 저장하는 객체이다.

4. nums를 순회하여 array의 $num - min$번째 Num 객체에 count를 증가시킨다.

5. array의 값들을 count 수로 내림차순 정렬한다.

6. result 변수는 k의 크기로 정의하고 array의 k번째 Num의 value를 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TopKFrequentElements.java){:target="_blank"}에서 확인 가능합니다.