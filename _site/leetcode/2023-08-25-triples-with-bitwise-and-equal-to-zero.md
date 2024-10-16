---
title: "Leetcode Java Triples with Bitwise AND Equal To Zero"
excerpt: "Leetcode Triples with Bitwise AND Equal To Zero Java"
last_modified_at: 2023-08-26T06:35:00
header:
  image: /assets/images/leetcode/triples-with-bitwise-and-equal-to-zero.png
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
[Link](https://leetcode.com/problems/triples-with-bitwise-and-equal-to-zero){:target="_blank"}

# 코드
```java
class Solution {

  public int countTriplets(int[] nums) {
    int[] count = new int[1 << 16];
    for (int num1 : nums) {
      for (int num2 : nums) {
        count[num1 & num2]++;
      }
    }
    int result = 0;
    for (int num : nums) {
      for (int i = 0; i < count.length; i++) {
        if ((num & i) == 0) {
          result += count[i];
        } else {
          i += (num & i) - 1;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/triples-with-bitwise-and-equal-to-zero/submissions/1031779378/){:target="_blank"}

# 설명
1. 아래의 조건을 만족하는 nums의 AND 배수의 수를 구하는 문제이다.
- AND의 삼중항인 (i, j, k)가 0 <= i, j, k < nums.length일 때, nums[i] & nums[j] & nums[k] == 0을 만족한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 문제 범위 내 만족하기 위한 기본 정수 배열을 저장할 변수로, 주어진 정수 범위 크기만큼 초기화하고 nums의 모든 값을 서로 반복하여 & 조건을 수행한 결과의 갯수를 count에 넣어준다.
- result는 조건에 만족하는 수를 계산할 변수로, 0으로 초기화한다.

3. nums의 모든 값을 num에 순차적으로 넣고 아래를 반복한다.
- 0부터 count의 길이 미만까지 i를 증가시키며 아래르 반복한다.
  - num과 i의 & 조건이 0인 경우, result에 해당 조건에 만족하는 갯수인 count[i]를 더해준다.
  - 그 외의 경우 i에 num과 i의 & 조건의 결과에 1을 뺀 값을 더해 만족할만한 위치로 i를 이동시켜준다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TriplesWithBitwiseANDEqualToZero.java){:target="_blank"}에서 확인 가능합니다.