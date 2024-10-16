---
title: "Leetcode Java Frequency of the Most Frequent Element"
excerpt: "Leetcode Frequency of the Most Frequent Element Java"
last_modified_at: 2023-11-18T17:50:00
header:
  image: /assets/images/leetcode/frequency-of-the-most-frequent-element.png
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
[Link](https://leetcode.com/problems/frequency-of-the-most-frequent-element){:target="_blank"}

# 코드
```java
class Solution {

  public int maxFrequency(int[] nums, int k) {
    int result = 1;
    int i = 0;
    int j = 0;
    Arrays.sort(nums);
    for (long sum = 0; j < nums.length; j++) {
      sum += nums[j];
      while (sum + k < (long) nums[j] * (j - i + 1)) {
        sum -= nums[i];
        i += 1;
      }
      result = Math.max(result, j - i + 1);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-unique-binary-string/submissions/1101293626/){:target="_blank"}

# 설명
1. 최대 k번 수행을 통해 nums 내 특정 값을 1씩 증가시킬 수 있는데, 연속으로 동일한 값이 되는 최대 길이를 구하는 문제이다.

2. nums를 오름차순으로 정렬 수행한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- result는 연속으로 동일한 값이 되는 최대 길이를 저장할 변수로, 0으로 초기화한다.
- sum은 이전 값을 저장해줄 변수로, overflow를 방지하기 위해서 Long 타입으로 정의 후 0으로 초기화한다.

4. i와 j를 0으로 초기화하고 j가 nums의 길이 미만일 때 까지 j를 증가시키며 아래를 반복한다.
- sum에 nums[j]의 값을 더해준다.
- $nums[j] \times (j - i + 1)$의 값이 $k + sum$보다 크면 더 증가시켜도 동일한 값이 되지 못하므로, sum에 nums[i]의 값을 빼고 i를 증가시켜준다.
- result에 result와 $j - i + 1$중 큰 값을 넣어 최대 길이를 저장한다.

5. 반복이 완료되면 최대 길이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FrequencyOfTheMostFrequentElement.java){:target="_blank"}에서 확인 가능합니다.