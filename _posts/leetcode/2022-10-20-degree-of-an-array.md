---
title: "Leetcode Java Count Binary Substrings"
excerpt: "Leetcode Count Binary Substrings Java"
last_modified_at: 2022-10-20T19:00:00
header:
  image: /assets/images/leetcode/degree-of-an-array.png
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
[Link](https://leetcode.com/problems/degree-of-an-array){:target="_blank"}

# 코드
```java
class Solution {

  public int findShortestSubArray(int[] nums) {
    int degree = 0;
    for (int num : nums) {
      degree = Math.max(degree, num);
    }
    int[] count = new int[degree + 1];
    int[] first = new int[degree + 1];
    int[] last = new int[degree + 1];
    int max = 1;
    for (int idx = 0; idx < nums.length; idx++) {
      count[nums[idx]]++;
      max = Math.max(max, count[nums[idx]]);
      if (first[nums[idx]] == 0) {
        first[nums[idx]] = idx + 1;
      }
      last[nums[idx]] = idx + 1;
    }
    int result = Integer.MAX_VALUE;
    for (int idx = 0; idx < count.length; idx++) {
      if (count[idx] == max) {
        result = Math.min(result, last[idx] - first[idx] + 1);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/826550429/){:target="_blank"}

# 설명
1. nums 내 최대 반복된 숫자를 포함한 연속된 부분 배열 중 가장 작은 배열의 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다. 
- degree는 nums 내 가장 큰 값을 넣기 위한 변수로, nums를 반복하여 가장 큰 값을 넣어준다.
- count는 nums 내 값들의 반복 횟수를 저장하기 위한 배열로, 최대 값까지 넣기 위해 $degree + 1$ 크기로 초기화한다.
- first는 nums 내 값의 시작 위치를, last는 nums 내 값의 마지막 위치를 저장하기 위한 배열로 count와 동일하게 최대 값까지 넣기 위해 $degree + 1$ 크기로 초기화한다.
- max는 가장 많이 반복된 횟수를 저장할 변수로, 1로 초기화한다.

3. nums의 모든 값을 이용하여 아래를 반복한다.
- count의 nums[idx] 번째 값을 증가시켜 발생 빈도를 저장한다.
- max에는 max와 count의 nums[idx] 번째 값 중 큰 값을 넣어 최대 발생 빈도를 저장한다.
- first의 nums[idx] 번째 값이 0인 경우, 처음 해당 값이 발생한 위치이므로 first의 nums[idx] 번째 위치에 $idx + 1$을 넣어준다.
- first의 nums[idx] 번째 값에 $idx + 1$을 넣어 마지막으로 발생한 위치를 기록한다.

4. 최소 길이를 저장할 result에 정수의 가장 큰 값을 넣어 초기화하고, count를 처음부터 반복하여 아래를 수행하여 result에 가장 작은 부분 배열의 길이를 저장한다.
- count[idx]가 최대 발생 횟수와 동일하면 result에 자기 자신과 마지막 발생 위치와 첫 발생 위치를 이용하여 길이를 계산해 넣어준다.

5. 모든 수행이 완료되면 가장 작은 부분 배열의 길이를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DegreeOfAnArray.java){:target="_blank"}에서 확인 가능합니다.