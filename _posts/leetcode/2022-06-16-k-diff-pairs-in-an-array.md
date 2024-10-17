---
title: "Leetcode Java K-diff Pairs in an Array"
excerpt: "Leetcode - 'K-diff Pairs in an Array' 문제 Java 풀이"
last_modified_at: 2022-06-16T20:00:00
header:
  image: /assets/images/leetcode/k-diff-pairs-in-an-array.png
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
[Link](https://leetcode.com/problems/k-diff-pairs-in-an-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int findPairs(int[] nums, int k) {
    Arrays.sort(nums);
    int slow = 0;
    int fast = 1;
    int count = 0;
    while (slow < nums.length && fast < nums.length) {
      if (slow == fast || nums[fast] - nums[slow] < k) {
        fast++;
      } else if (nums[fast] - nums[slow] > k) {
        slow++;
      } else {
        slow++;
        fast++;
        count++;
        while (slow < nums.length && nums[slow] == nums[slow - 1]) {
          slow++;
        }
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/723572278/){:target="_blank"}

# 설명
1. nums와 k의 고유한 k-diff 쌍의 수를 계산하는 문제이다.
- k-diff 쌍인 nums[i], nums[j]는 아래를 만족한다.
  - 0 <= i, j < nums.length
  - i != j
  - nums[i] - nums[j] == k

2. 순차적인 차이를 계산하기 위해 nums를 오름차순으로 정렬해준다.

3. 문제 풀이에 필요한 변수를 정의한다.
- slow는 작은 값의 위치를 이동하며 탐색할 변수로, 0으로 초기화한다.
- fast는 slow보다 큰 값의 위치를 이동하며 탐색할 변수로, slow보다 큰 1로 초기화한다.
- count는 k-diff 쌍의 수를 세기위한 변수로, 0으로 초기화한다.

4. slow 혹은 fast가 nums의 길이보다 커지기 전까지 아래의 반복을 수행한다.
- slow와 fast가 동일하거나 nums[fast]에 nums[slow]를 뺀 값이 k보다 작을 경우, 더 큰 차잇값을 계산하기 위해서 fast를 증가시킨다.
- 위의 경우가 아니면서 nums[fast]에 nums[slow]를 뺀 값이 k보다 큰 경우, 더 작은 차잇값을 계산하기 위해서 slow를 증가시킨다.
- 그게 아니라면 nums[fast]에 nums[slow]를 뺀 값이 k와 동일하므로, slow와 fast와 count를 모두 증가시키고 slow가 마지막 값이 아니면서 이전 값과 동일한 경우가 아닐 때 까지 slow를 증가시킨다.

5. 반복이 완료되면 k-diff 쌍의 수를 계산한 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KdiffPairsInAnArray.java){:target="_blank"}에서 확인 가능합니다.