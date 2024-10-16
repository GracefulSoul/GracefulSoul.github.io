---
title: "Leetcode Java Find Unique Binary String"
excerpt: "Leetcode Find Unique Binary String Java"
last_modified_at: 2023-11-16T19:40:00
header:
  image: /assets/images/leetcode/find-unique-binary-string.png
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
[Link](https://leetcode.com/problems/find-unique-binary-string){:target="_blank"}

# 코드
```java
class Solution {

  public String findDifferentBinaryString(String[] nums) {
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < nums.length; i++) {
      sb.append(nums[i].charAt(i) == '0' ? '1' : '0');
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-unique-binary-string/submissions/1100093000/){:target="_blank"}

# 설명
1. nums와 중복되지 않은 임의의 이진 값을 찾는 문제이다.
- nums[i]의 길이와 nums의 길이와 같으며, 여러 값이 존재하면 임의 하나의 값을 반환한다.

2. sb는 결과를 저장할 변수로, 동적인 문자열 생성을 위해 StringBuilder로 초기화한다.

3. 0부터 length까지 i를 증가시키면서 nums[i]의 i번째 문자가 0이면 1로, 1이면 0으로 반전시킨다.

4. 중복되지 않은 임의 이진 값이 저장된 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindUniqueBinaryString.java){:target="_blank"}에서 확인 가능합니다.