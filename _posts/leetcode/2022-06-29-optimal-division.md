---
title: "Leetcode Java Optimal Division"
excerpt: "Leetcode Optimal Division Java"
last_modified_at: 2022-06-29T20:30:00
header:
  image: /assets/images/leetcode/optimal-division.png
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
[Link](https://leetcode.com/problems/optimal-division/){:target="_blank"}

# 코드
```java
class Solution {

  public String optimalDivision(int[] nums) {
    int length = nums.length;
    StringBuilder sb = new StringBuilder();
    sb.append(nums[0]);
    for (int idx = 1; idx < length; idx++) {
      sb.append("/");
      if (idx == 1 && length > 2) {
        sb.append("(");
      }
      sb.append(nums[idx]);
    }
    if (length > 2) {
      sb.append(")");
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/734199084/){:target="_blank"}

# 설명
1. 정수가 들어있는 nums를 나눗셈만 사용해서 나올 수 있는 최대의 값을 구하는 공식을 만들어 반환하는 문제이다.
- 수학 공식을 나눗셈만 사용하여 계산할 경우 나올 수 있는 최솟값과 최댓값은 아래와 같다.
  - 모든 값을 순차적으로 나눈 결과는 최솟값이 된다. (Ex. $1 / 2 / 3 / 4 = \frac{1}{2} / 3 / 4 = \frac{1}{6} / 4 = \frac{1}{24}$)
  - 첫 값을 나머지 값들을 순차적으로 나눈 결과로 나눈 결과는 최댓값이 된다. (Ex. $1 / (2 / 3 / 4) = 1 / (\frac{2}{3} / 4) = 1 / \frac{2}{12} = \frac{12}{2} = 6$)

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- sb는 주어진 문제의 공식을 동적으로 구성할 StringBuilder 객체로 정의하고, nums의 첫 값을 넣어준다.
  - 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.

3. 1부터 length 미만까지 idx를 증가시키며 아래를 수행한다.
- sb에 나눗셈 기호("/")를 추가한다.
- idx가 1이고 length가 2 초과인 경우, 소괄호 시작 문자("(")를 추가한다.
- sb에 nums의 idx번쨰 값을 넣어준다.

4. 반복이 완료되고 length가 2 초과인 경우, 소괄호 종료 문자(")")를 추가한다.

5. 완성된 공식인 sb를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/OptimalDivision.java){:target="_blank"}에서 확인 가능합니다.