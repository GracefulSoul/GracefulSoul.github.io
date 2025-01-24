---
title: "Leetcode Java Maximum Equal Frequency"
excerpt: "Leetcode - 'Maximum Equal Frequency' 문제 Java 풀이"
last_modified_at: 2025-01-24T09:55:00
header:
  image: /assets/images/leetcode/maximum-equal-frequency.png
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
[Link](https://leetcode.com/problems/maximum-equal-frequency/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxEqualFreq(int[] nums) {
    int[] counts = new int[100001];
    int[] frequencies = new int[100001];
    int length = nums.length;
    int result = 0;
    for (int i = 0; i < length; i++) {
      counts[nums[i]]++;
      int frequency = counts[nums[i]];
      frequencies[frequency]++;
      int count = frequencies[frequency] * frequency;
      if (count == i + 1 && i != length - 1) {
        result = Math.max(result, i + 2);
      } else if (count == i) {
        result = Math.max(result, i + 1);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-equal-frequency/submissions/1518517607/){:target="_blank"}

# 설명
1. 양의 정수가 들어있는 배열인 nums의 부분 배열 중 한 값을 제거하여 동일한 값이 정확히 같은 횟수로 반복되는 부분 배열의 최대 길이를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- counts와 frequencies는 문자 갯수와 빈도를 계산하기 위한 변수로, 각각 최대 크기인 $10^5$ 보다 1 큰 크기의 정수 배열로 초기화한다.
- length는 nums의 길이를 저장한 변수이다.
- result는 부분 배열의 길이를 저장한 변수로, 0으로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- counts[nums[i]]의 값인 nums[i]번째 문자 갯수를 증가시킨다.
- frequency는 현재 발생 빈도 기준을 저장할 변수로, counts[nums[i]]의 값을 넣어준다.
- frequencies[frequency]의 값을 증가시켜 현재까지 문자 발생 빈도의 갯수를 증가시켜준다.
- count는 현재 발생 빈도만큼의 문자열이 동일하게 발생한 경우, 문자의 갯수를 저장한 변수이다.
- count가 $i + 1$과 동일하면서 $length - 1$인 마지막 위치가 아닌 경우, result에 result와 $i + 2$인 현재까지 부분 문자열 길이보다 1 큰 값 중 큰 값을 넣어준다.
  - nums의 값이 [1, 1, 3, 3, 5] 인 경우, 전체를 부분 배열로 하면 조건을 만족하는 1과 3이 존재하면서 제거할 5가 있으므로 count가 $i + 1$과 동일하다.
  - i는 0-index이므로 길이는 1을 더한 값이다.
- 위의 경우가 아니면서 count가 i와 동일한 경우, result에 result와 $i + 1$ 중 큰 값을 넣어준다.
  - nums의 값이 [1, 1, 3, 3, 3, 5] 인 경우, 조건을 만족하는 범위인 [1, 1, 3, 3, 3]인 부분 배열에서 3만 제거하면 되므로 count가 i와 동일하다.

4. 반복이 완료되면 부분 배열의 최대 길이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumEqualFrequency.java){:target="_blank"}에서 확인 가능합니다.