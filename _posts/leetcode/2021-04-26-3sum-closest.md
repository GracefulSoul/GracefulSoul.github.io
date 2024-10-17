---
title: "Leetcode Java 3sum Closest"
excerpt: "Leetcode - '3sum Closest' 문제 Java 풀이"
last_modified_at: 2021-04-26T22:00:00
header:
  image: /assets/images/leetcode/3sum-closest.png
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
[Link](https://leetcode.com/problems/3sum-closest/){:target="_blank"}

# 코드
```java
class Solution {

  public int threeSumClosest(int[] nums, int target) {
    Arrays.sort(nums);
    int result = nums[0] + nums[1] + nums[nums.length - 1];
    for (int idx = 0; idx < nums.length - 2; idx++) {
      int start = idx + 1;
      int end = nums.length - 1;
      while (start < end) {
        int sum = nums[idx] + nums[start] + nums[end];
        if (Math.abs(target - result) > Math.abs(target - sum)) {
          result = sum;
        }
        if (sum > target) {
          end--;
        } else {
          start++;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/485417150/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums를 오름차순 정렬한다.

2. 주어진 정수 target의 인접한 세 값의 합을 저장할 result 변수의 초기값을 $nums[0] + nums[1] + nums[nums.length - 1]$로 초기화 한다.
- 임의의 값을 부여하면, target의 값과 유사한 값이 초기 값으로 설정될 수 있으므로 반복의 첫 값으로 초기화한다.

3. 반복을 통해 첫 값을 제외한 두 pointer의 역할을 수행할 변수 start는 $idx + 1$로, 변수 end는 $nums.length - 1$로 설정해서 첫 pointer인 idx 이후의 값을 순차 탐색할 수 있도록 한다.
- 반복은 start 변수의 값이 end 변수의 값보다 작을(마주치지 않을) 때까지 반복한다.
- 임시로 세 pointer의 배열 값을 더하여 sum 변수를 설정한다.
- 만일 $target - result$의 절대값이 $target - sum$ 보다 클 경우에 result 변수에 sum 변수의 값을 주입한다.
- 만일 sum 변수의 값이 target의 값보다 크면 작은 값을 더해야 하므로 변수 end의 값을 내리고, 그렇지 않으면 변수 start의 값을 올려 더 큰 값을 더할 수 있도록 하여 반복을 계속 수행한다.

4. 반복이 완료되면 세 값의 합이 target과 가장 인접한 result 변수를 주어진 문제의 결과로 반환한다.    

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ThreeSumClosest.java){:target="_blank"}에서 확인 가능합니다.