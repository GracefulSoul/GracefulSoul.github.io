---
title: "Leetcode Java Find All Numbers Disappeared in an Array"
excerpt: "Leetcode - 'Find All Numbers Disappeared in an Array' 문제 Java 풀이"
last_modified_at: 2022-04-07T13:00:00
header:
  image: /assets/images/leetcode/find-all-numbers-disappeared-in-an-array.png
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
[Link](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> findDisappearedNumbers(int[] nums) {
    List<Integer> result = new ArrayList<>();
    int[] count = new int[nums.length + 1];
    for (int num : nums) {
      count[num]++;
    }
    for (int idx = 1; idx < count.length; idx++) {
      if (count[idx] == 0) {
        result.add(idx);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/675507442/){:target="_blank"}

# 설명
1. 정수 배열 nums에서 1부터 해당 배열의 길이까지 숫자 중 누락된 숫자들을 찾아 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 누락된 숫자를 넣을 변수로, ArrayList로 초기화한다.
- count는 nums 내 포함된 숫자의 개수를 세기 위한 변수로, nums의 길이보다 하나 크게 정의한다.

3. nums를 반복하여 count의 num번째 위치의 값을 증가시킨다.

4. 1부터 count의 길이 미만까지 idx를 증가시키며 반복하여 아래를 수행한다.
- count의 idx번째 값이 0인 경우, nums에 미 포함된 값이므로 result에 포함시킨다.

5. 반복을 통해 누락된 숫자들을 추가한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindAllNumbersDisappearedInAnArray.java){:target="_blank"}에서 확인 가능합니다.