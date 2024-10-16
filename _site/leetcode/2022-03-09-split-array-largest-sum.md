---
title: "Leetcode Java Split Array Largest Sum"
excerpt: "Leetcode Split Array Largest Sum Java 풀이"
last_modified_at: 2022-03-09T11:00:00
header:
  image: /assets/images/leetcode/split-array-largest-sum.png
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
[Link](https://leetcode.com/problems/split-array-largest-sum/){:target="_blank"}

# 코드
```java
class Solution {

  public int splitArray(int[] nums, int m) {
    int max = 0;
    int sum = 0;
    for (int num : nums) {
      max = Math.max(max, num);
      sum += num;
    }
    while (max < sum) {
      int mid = max + (sum - max) / 2;
      if (this.isValid(nums, m, mid)) {
        sum = mid;
      } else {
        max = mid + 1;
      }
    }
    return max;
  }

  private boolean isValid(int[] nums, int m, int mid) {
    int sum = 0;
    int count = 1;
    for (int num : nums) {
      sum += num;
      if (sum > mid) {
        count++;
        sum = num;
        if (count > m) {
          return false;
        }
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/656206564/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums를 이용하여 아래의 조건을 만족하는 부분 배열 내 가장 큰 값을 구하는 문제이다.
- nums를 m개의 부분 배열로 분리하는 여러 경우 중 부분 배열의 합이 최대인 값이 최소가 되는 경우를 구한다.
- 모든 부분 배열은 비어있지 않아야 한다.

2. nums 배열의 가장 큰 값을 max에, 모든 값의 합을 sum에 정의한다.

3. max가 sum보다 작을 때 까지 반복한다.
- 최댓값의 상한을 정하는 mid에 $max + \frac{sum - max}{2}$의 값을 넣어준다.
- 4번에서 정의한 isValid(int[] nums, int m, int mid) 메서드의 수행 결과에 따라 아래를 수행한다.
  - 결과가 true인 경우 부분 배열로 분리할 수 있으므로, sum에 mid 값을 넣어 최댓값의 상한 축소시킨다.
  - 결과가 false인 경우 부분 배열로 분리할 수 없으므로, max에 $mid + 1$의 값을 최댓값의 상한을 확장시킨다.

4. 부분 배열롤 분리할 수 있는지 여부를 판단하기 위한 isValid(int[] nums, int m, int mid) 메서드를 완성한다.
- 문제 풀이에 필요한 변수를 정의한다.
  - sum은 부분 배열의 합계를 계산하기 위한 변수로, 0으로 초기화한다.
  - count는 부분 배열의 개수를 계산하기 위한 변수로, 1로 초기화한다.
- nums를 처음부터 끝까지 반복한다.
  - sum에 num을 더해주고, sum이 mid보다 큰 경우 부분 배열 분리가 가능하므로 아래를 수행한다.
    - count를 증가시켜 부분 배열의 개수를 추가한다.
    - sum에 num을 넣어 부분 배열의 값을 초기화 시킨다.
    - 만일 count가 m보다 큰 경우 목표하고자 하는 부분 배열의 크기를 초과하였으므로, false를 반환한다.
- 반복이 완료되면 목표하고자 하는 부분 배열의 크기를 만족하는 분리가 가능하므로, true를 반환한다.

5. 3번의 반복이 완료되면 요구 조건을 만족하는 부분 배열 내 가장 큰 값을 저장한 max를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SplitArrayLargestSum.java){:target="_blank"}에서 확인 가능합니다.