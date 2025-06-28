---
title: "Leetcode Java Find Subsequence of Length K With the Largest Sum"
excerpt: "Leetcode - 'Find Subsequence of Length K With the Largest Sum' 문제 Java 풀이"
last_modified_at: 2025-06-28T11:20:00
header:
  image: /assets/images/leetcode/find-subsequence-of-length-k-with-the-largest-sum.png
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
[Link](https://leetcode.com/problems/find-subsequence-of-length-k-with-the-largest-sum/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] maxSubsequence(int[] nums, int k) {
    int length = nums.length;
    int[] sorted = Arrays.copyOf(nums, length);
    Arrays.sort(sorted);
    int limit = sorted[length - k];
    int count = 0;
    for (int i = length - k; i < length; i++) {
      if (sorted[i] == limit) {
        count++;
      }
    }
    int[] result = new int[k];
    int i = 0;
    for (int num : nums) {
      if (num > limit) {
        result[i++] = num;
      } else if (num == limit && count > 0) {
        result[i++] = num;
        count--;
      }
      if (i == k) {
        break;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-subsequence-of-length-k-with-the-largest-sum/submissions/1678803522/){:target="_blank"}

# 설명
1. 정수 배열 nums에서 순차적인 k개 숫자들의 합이 최대인 부분 수열을 만드는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- sorted는 nums의 값들을 오름차순 정렬한 배열로 저장할 변수로, nums를 깊은 복제를 수행 후 오름차순 정렬해준다.
- limit은 sorted 내 제거할 숫자의 한계 값을 저장할 변수로, sorted[$length - k$]의 포함될 첫 숫자의 값으로 초기화한다.
- count는 limit과 동일한 숫자의 갯수를 계산할 변수로, sorted 내 $length - k$부터 마지막 위치까지 값들 중 limit과 동일한 값의 갯수를 넣어준다.
- result는 k개 숫자의 합이 최대인 부분 수열을 저장할 변수로, k 크기의 정수 배열로 초기화한다.
- i는 result내 위치 변수로, 0으로 초기화한다.

3. nums의 각 값을 순차적으로 num에 넣어 아래를 수행한다.
- num이 limit보다 큰 부분 수열에 포함되는 숫자의 경우, result[i]에 num을 넣어주고 i를 증가시켜준다.
- num이 limit과 동일하면서 count가 0 초과인 포함될 숫자의 경우, result[i]에 num을 넣어주고 i를 증가 count를 감소시켜준다.
- 위의 수행 이후 i가 k와 동일한 부분 수열이 완성된 경우, 반복을 중지한다.

4. 3번의 반복을 통해 완성된 부분 수열인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindSubsequenceOfLengthKWithTheLargestSum.java){:target="_blank"}에서 확인 가능합니다.