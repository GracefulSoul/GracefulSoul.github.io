---
title: "Leetcode Java Arithmetic Slices"
excerpt: "Leetcode Arithmetic Slices Java 풀이"
last_modified_at: 2022-03-13T15:00:00
header:
  image: /assets/images/leetcode/arithmetic-slices.png
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
[Link](https://leetcode.com/problems/arithmetic-slices/){:target="_blank"}

# 코드
```java
class Solution {

  public int numberOfArithmeticSlices(int[] nums) {
    int number = 0;
    int count = 0;
    for (int idx = 2; idx < nums.length; idx++) {
      if (nums[idx] - nums[idx - 1] == nums[idx - 1] - nums[idx - 2]) {
        count++;
        number += count;
      } else {
        count = 0;
      }
    }
    return number;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/658973072/){:target="_blank"}

# 설명
1. 주어진 정수 배열인 num을 이용하여 최소 3개 이상의 연속된 숫자의 차이가 동일한 부분 배열을 만들 수 있는 최대 부분 배열의 갯수를 산정하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- number는 최소 3개 이상의 연속된 숫자의 차이가 동일한 부분 배열의 갯수를 저장하는 변수로, 0으로 초기화한다.
  - 간단히 [1, 2, 3, 4]의 경우 아래의 예제이다.
    - 첫 번째 수행에 부분 배열인 [1, 2, 3]을 만들 수 있으므로 1개이다.
    - 두 번쨰 수행에 부분 배열인 [2, 3, 4]를 만들 수 있고, 첫 번째 수행에 이어지므로 [1, 2, 3, 4]의 부분 배열도 생성이 가능하므로 2개가 된다.
    - 위의 수행으로 총 3개의 부분 배열을 생성 할 수 있다.
- count는 연속된 숫자의 차이가 동일한 경우 만들 수 있는 부분 배열의 갯수를 임시 산정하는 변수로, 0으로 초기화한다.

3. 2부터 nums의 길이만큼 idx를 증가시키며 아래를 수행한다.
- nums의 현재 위치와 그 전 위치의 값의 차이가 그 전 위치와 그 전의 전 위치의 값의 차이가 동일한 경우 최소 3개 이상의 연속된 숫자의 차이가 동일하므로, count를 증가시키고 number에 count를 더해준다.
- 그렇지 않은 경우, 연속되지 않으므로 count를 초기화 시킨다.

4. 반복이 완료되면 최소 3개 이상의 연속된 숫자의 차이가 동일한 부분 배열을 만들 수 있는 최대 부분 배열의 갯수인 number를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ArithmeticSlices.java){:target="_blank"}에서 확인 가능합니다.