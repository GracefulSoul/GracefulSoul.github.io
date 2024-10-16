---
title: "Leetcode Java Sum of Absolute Differences in a Sorted Array"
excerpt: "Leetcode Sum of Absolute Differences in a Sorted Array Java"
last_modified_at: 2023-11-25T18:40:00
header:
  image: /assets/images/leetcode/sum-of-absolute-differences-in-a-sorted-array.png
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
[Link](https://leetcode.com/problems/sum-of-absolute-differences-in-a-sorted-array){:target="_blank"}

# 코드
```java
class Solution {

  public int[] getSumAbsoluteDifferences(int[] nums) {
    int length = nums.length;
    int[] result = new int[length];
    int[] sum = new int[length + 1];
    for (int i = 0; i < length; i++) {
      sum[i + 1] = sum[i] + nums[i];
    }
    for (int i = 0; i < length; i++) {
      result[i] = (i * nums[i]) - sum[i] + (sum[length] - sum[i] - ((length - i) * nums[i]));
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sum-of-absolute-differences-in-a-sorted-array/submissions/1105812466/){:target="_blank"}

# 설명
1. nums의 각 자리 별 모든 값의 차잇값에 대한 절댓값을 더해서 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- result는 각 자리 별 모든 값의 차잇값에 대한 절댓값을 더한 값을 저장하기 위한 변수로, length 길이의 정수 배열로 초기화한다.
- sum은 누계하기 위한 변수로, $length + 1$ 크기의 정수 배열로 초기화하고 $i + 1$ 위치에 i번째 값까지의 누계를 넣어준다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- result[i]에 아래의 값들을 더해준다.
  - i번째 값 이전까지의 결과는 $(nums[i] - num[0]) + (nums[i] - nums[1]) + ... + (nums[i] - nums[i - 1]) = (i \times nums[i]) - sum[i]$이다.
  - i번째 값에는 같은 값끼리 빼기 때문에 0이 된다.
  - i번쨰 값 이후부터의 결과는 처음과 같이 하면 음수가 되기 때문에, 반대로 이후 값부터 빼므로 $(nums[i + 1] - nums[i]) + (nums[i + 2] - nums[i]) + ... + (nums[length - 1] - nums[i]) = sum[length] - sum[i] - ((length - i) * nums[i])$이 된다.

4. 계산된 결과가 담긴 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SumOfAbsoluteDifferencesInASortedArray.java){:target="_blank"}에서 확인 가능합니다.