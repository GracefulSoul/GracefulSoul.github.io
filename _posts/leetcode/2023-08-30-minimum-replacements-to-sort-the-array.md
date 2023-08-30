---
title: "Leetcode Java Minimum Replacements to Sort the Array"
excerpt: "Leetcode Minimum Replacements to Sort the Array Java"
last_modified_at: 2023-08-30T20:20:00
header:
  image: /assets/images/leetcode/minimum-replacements-to-sort-the-array.png
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
[Link](https://leetcode.com/problems/minimum-replacements-to-sort-the-array){:target="_blank"}

# 코드
```java
class Solution {

  public long minimumReplacement(int[] nums) {
    int length = nums.length;
    int last = nums[length - 1];
    long result = 0;
    for (int i = length - 2; i >= 0; i--) {
      int time = nums[i] / last;
      if (nums[i] % last != 0) {
        last = nums[i] / ++time;
      }
      result += time - 1;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-replacements-to-sort-the-array/submissions/1035887660/){:target="_blank"}

# 설명
1. nums의 값들을 $a = b + c$를 만족하는 b와 c의 두 값으로 분리하여 감소하지 않는 배열을 만드는데 필요한 최소 횟수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 값을 저장한 변수이다.
- last는 감소하지 않는 추세로 변환하기 위해 이전 값을 저장할 변수로, nums의 마지막 값을 넣어준다.
- result는 분리 횟수를 저장할 변수이다.

3. $length - 2$부터 0 이상까지 i를 증가시키며 역순으로 아래를 반복한다.
- time에 last의 값을 넘지 않는 수준까지 나눠야 할 횟수인 $\frac{nums[i]}{last}$ 값을 저장한다.
- nums[i]를 last로 나눈 나머지가 0이 아닌 경우, last에 time을 증가시킨 값으로 nums[i]를 나눈 값을 넣어준다.
- result의 분리 횟수인 $time - 1$을 더해준다.

4. 반복이 완료되면 최소 분리 횟수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumReplacementsToSortTheArray.java){:target="_blank"}에서 확인 가능합니다.