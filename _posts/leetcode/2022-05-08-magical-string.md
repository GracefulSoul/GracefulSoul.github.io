---
title: "Leetcode Java Magical String"
excerpt: "Leetcode - 'Magical String' 문제 Java 풀이"
last_modified_at: 2022-05-08T19:00:00
header:
  image: /assets/images/leetcode/magical-string.png
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
[Link](https://leetcode.com/problems/magical-string/){:target="_blank"}

# 코드
```java
class Solution {

  public int magicalString(int n) {
    int fast = 1;
    int slow = 1;
    int num = 1;
    int[] nums = new int[n + 2];
    while (fast <= n) {
      nums[fast++] = num;
      if (nums[slow++] == 2) {
        nums[fast++] = num;
      }
      num = 3 - num;
    }
    int count = 0;
    for (int idx = 1; idx <= n; idx++) {
      if (nums[idx] == 1) {
        count++;
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/695418469/){:target="_blank"}

# 설명
1. 1과 2로 이루어진 아래의 규칙에 의해 생성된 문자열 s의 n 번째 자리까지 존재하는 1의 개수를 구하는 문제이다.
- 문자열 s는 "1221121221221121122..." 형태로 이루어지며, 그룹화하면 "1 22 11 2 1 22 1 22 11 2 11 22 ..."으로 표현이 된다.
- 각 그룹의 1 또는 2의 발생 순서는 "1 2 2 1 1 2 1 2 2 1 2 2 ..."으로 볼 수 있다.
- 이는 각 숫자가 반전이 될 때 $num = 3 - num$로 뒤집어 줄 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- fast와 slow는 문자열 s를 구성하기 위한 인덱스로, 1로 초기화한다.
  - fast는 현재 커서의 인덱스로 nums 내 값을 넣기 위한 변수이다.
  - slow는 검증을 위한 인덱스로 nums 의 slow번째 값이 2인 경우, fast의 다음 자리에 num을 한 번 더 넣어주는 역할을 수행하여 위의 규칙을 만족하는 문자열 s를 만들 수 있다.
- num은 문자열 s의 각 위치에 들어갈 숫자로, 첫 값인 1로 초기화한다.
- nums는 문자열 s를 구성하기 위한 배열로, $n + 2$ 크기로 초기화한다.

3. fast가 n 이하일 때 까지 아래를 수행하여 문자열 s의 각 자리 숫자를 nums에 차례대로 넣어준다.
- nums의 fast번째 자리에 num을 넣고 fast를 증가시킨다.
- nums의 slow번째 값이 2인지 검증하고 slow를 증가시키고, 2가 맞는 경우 nums의 fast번째 값에 num을 넣어주고 fast를 증가시킨다.
- num에 $3 - num$을 넣어 숫자를 뒤집어준다.

4. count를 0으로 초기화 시키고, nums를 반복하여 1의 개수를 count에 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MagicalString.java){:target="_blank"}에서 확인 가능합니다.