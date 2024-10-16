---
title: "Leetcode Java Find All Duplicates in an Array"
excerpt: "Leetcode Find All Duplicates in an Array Java 풀이"
last_modified_at: 2022-04-02T13:00:00
header:
  image: /assets/images/leetcode/find-all-duplicates-in-an-array.png
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
[Link](https://leetcode.com/problems/find-all-duplicates-in-an-array/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> findDuplicates(int[] nums) {
    List<Integer> result = new ArrayList<>();
    int[] count = new int[nums.length];
    for (int num : nums) {
      count[num - 1]++;
    }
    for (int idx = 0; idx < count.length; idx++) {
      if (count[idx] == 2) {
        result.add(idx + 1);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/671967231/){:target="_blank"}

# 설명
1. 정수 배열 nums 내 중복된 값을 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 중복된 정수를 저장하기 위한 변수로, ArrayList로 정의한다.
- count는 중복된 값을 찾기 위한 변수로, nums의 길이만큼의 크기로 초기화한다.

3. nums를 반복하여 count의 $num - 1$ 위치의 값을 증가시킨다.

4. count를 반복하여, count가 2인 값들을 result에 넣어준다.

5. 중복된 값들을 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindAllDuplicatesInAnArray.java){:target="_blank"}에서 확인 가능합니다.