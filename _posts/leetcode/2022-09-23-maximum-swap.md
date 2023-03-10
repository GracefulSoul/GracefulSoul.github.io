---
title: "Leetcode Java Maximum Swap"
excerpt: "Leetcode Maximum Swap Java"
last_modified_at: 2022-09-23T19:30:00
header:
  image: /assets/images/leetcode/maximum-swap.png
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
[Link](https://leetcode.com/problems/maximum-swap){:target="_blank"}

# 코드
```java
class Solution {

  public int maximumSwap(int num) {
    char[] numCharArray = Integer.toString(num).toCharArray();
    int length = numCharArray.length;
    int[] nums = new int[10];
    for (int idx = 0; idx < length; idx++) {
      nums[numCharArray[idx] - '0'] = idx;
    }
    for (int i = 0; i < length; i++) {
      for (int j = 9; j > numCharArray[i] - '0'; j--) {
        if (nums[j] > i) {
          char temp = numCharArray[i];
          numCharArray[i] = numCharArray[nums[j]];
          numCharArray[nums[j]] = temp;
          return Integer.valueOf(new String(numCharArray));
        }
      }
    }
    return num;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/806751825/){:target="_blank"}

# 설명
1. num의 모든 숫자를 이용하여 최대 한 번만 숫자를 변경하여 가장 큰 숫자를 만드는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- numCharArray는 num의 각 자리수를 순차적인 문자 배열로 전환하여 저장한 변수이다.
- length는 numCharArray의 길이를 저장한 변수이다.
- nums는 각 숫자의 마지막 위치를 저장할 배열로, 0 ~ 9 까지 10개이므로 해다 개수만큼의 크기로 초기화하고 numCharArray를 모두 반복하여 발생한 숫자의 마지막 위치를 넣어준다.

3. 0부터 length까지 i를 증가시키고, 9부터 $numCharArray[i] - '0'$인 numCharArray의 i번째 문자를 숫자로 변환한 값 미만까지 j를 감소시키며 아래를 반복한다.
- nums의 j에 해당하는 위치가 i보다 큰 경우 현재 자리보다 큰 값이 존재하므로, numCharArray의 i번째 값과 nums[j]번째 값의 위치를 변경해주고 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 현재 숫자가 가장 큰 숫자이므로, num을 그대로 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumSwap.java){:target="_blank"}에서 확인 가능합니다.