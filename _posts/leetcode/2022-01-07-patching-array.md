---
title: "Leetcode Java Patching Array"
excerpt: "Leetcode Patching Array Java 풀이"
last_modified_at: 2022-01-07T12:00:00
header:
  image: /assets/images/leetcode/patching-array.png
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
[Link](https://leetcode.com/problems/patching-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int minPatches(int[] nums, int n) {
    int length = nums.length;
    int miss = 1;
    int count = 0;
    for (int idx = 0; 0 < miss && miss <= n;) {
      if (idx < length && nums[idx] <= miss) {
        miss += nums[idx++];
      } else {
        miss += miss;
        count++;
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/614611959/){:target="_blank"}

# 설명
1. 주어진 배열 nums의 값들을 이용하여 부분 배열의 합이 1 ~ n까지 가능하기 위해, nums에 추가할 숫자의 개수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length 는 주어진 배열 nums의 길이를 저장할 변수로, nums.length를 넣어준다.
- miss는 추가할 숫자를 저장할 변수로, 첫 값은 1로 넣어준다.
- count는 추가할 숫자의 개수를 저장할 변수로, 0으로 초기화한다.

3. miss가 0부터 0보다 크고 n보다 작거나 같을 때까지 idx를 증가시키며 반복하여 아래를 수행한다.
- idx가 length보다 작고 nums의 idx번째 값이 miss보다 작을 경우, miss에 nums[idx] 값을 추가하고 idx를 증가시킨다.
- 위의 경우가 아닌 경우, miss에 miss를 더해주고 count를 증가시킨다.

4. 반복이 완료되면 nums의 값들을 이용하여 부분 배열의 합이 1 ~ n까지 가능하기 위해, nums에 추가할 숫자의 개수를 계산한 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PatchingArray.java){:target="_blank"}에서 확인 가능합니다.