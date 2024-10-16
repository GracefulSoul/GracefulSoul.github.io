---
title: "Leetcode Java Sum of Even Numbers After Queries"
excerpt: "Leetcode Sum of Even Numbers After Queries Java"
last_modified_at: 2023-09-03T10:40:00
header:
  image: /assets/images/leetcode/sum-of-even-numbers-after-queries.png
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
[Link](https://leetcode.com/problems/sum-of-even-numbers-after-queries){:target="_blank"}

# 코드
```java
class Solution {

  public int[] sumEvenAfterQueries(int[] nums, int[][] queries) {
    int sum = 0;
    for (int num : nums) {
      if (num % 2 == 0) {
        sum += num;
      }
    }
    int[] result = new int[queries.length];
    for (int i = 0; i < queries.length; i++) {
      int[] query = queries[i];
      if (nums[query[1]] % 2 == 0) {
        sum -= nums[query[1]];
      }
      nums[query[1]] += query[0];
      if (nums[query[1]] % 2 == 0) {
        sum += nums[query[1]];
      }
      result[i] = sum;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sum-of-even-numbers-after-queries/submissions/1038968032/){:target="_blank"}

# 설명
1. nums의 값들을 이용해 queries로 값을 변경한 순서대로 짝수의 값들의 합을 반환하는 문제이다.
- queries[i] = [value, index]로 구성이 되며, i번째 query는 nums[index]의 값에 value를 더해준다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 짝수의 합을 저장할 변수로, nums의 모든 값들 중 짝수만 찾아 더해준다.
- result는 query 수행 후 짝수의 합을 저장할 변수로, query의 수행 횟수인 queries의 길이만큼의 크기로 초기화한다.

3. 0부터 queries의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- query에 queries의 i번째 배열을 넣어준다.
- nums에서 query[1]의 값인 위치에 해당하는 값이 짝수이면 sum에서 해당 값을 빼준다.
- nums에서 query[1]의 값인 위치에 해당하는 값에 query[0]의 값을 더해준다.
- nums에서 query[1]의 값인 위치에 해당하는 값이 짝수인지 다시 검증하여 sum에 해당 값을 더해준다.
- result[i]에 위를 수행하여 저장된 짝수의 합인 sum을 넣어준다.

4. 반복이 완료되어 저장된 결과인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SumOfEvenNumbersAfterQueries.java){:target="_blank"}에서 확인 가능합니다.