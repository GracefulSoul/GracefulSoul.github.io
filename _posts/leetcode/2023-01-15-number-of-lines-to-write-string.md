---
title: "Leetcode Java Number of Lines To Write String"
excerpt: "Leetcode Number of Lines To Write String Java"
last_modified_at: 2023-01-15T10:00:00
header:
  image: /assets/images/leetcode/number-of-lines-to-write-string.png
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
[Link](https://leetcode.com/problems/number-of-lines-to-write-string){:target="_blank"}

# 코드
```java
class Solution {

  public int[] numberOfLines(int[] widths, String s) {
    int[] result = new int[] { 1, 0 };
    for (char c : s.toCharArray()) {
      int curr = widths[c - 'a'];
      if (result[1] + curr > 100) {
        result[0]++;
        result[1] = curr;
      } else {
        result[1] += curr;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-lines-to-write-string/submissions/878304072/){:target="_blank"}

# 설명
1. 각 영문자 별 길이를 저장한 widths를 이용하여 각 라인 별 길이가 100을 넘지 않도록 문자열 s를 개행 처리하였을 때, [행의 수, 마지막 줄의 길이] 형태의 배열을 반환하는 문제이다.

2. result는 결과를 저장할 변수로, 첫 행의 수와 초기 길이인 [1, 0]으로 초기화한다.

3. s의 각 문자를 c에 넣어 아래를 반복한다.
- curr은 현재 문자인 c의 길이를 widths에서 찾아 넣어준다.
- result[1]인 현재 길이와 curr의 합이 100을 초과하는 경우, 행의 수인 result의 첫 번째 값을 증가시키고 현재 행의 길이인 result의 두 번째 값에 curr을 넣어 새로운 행의 길이를 초기화 시켜준다.
- 위의 경우가 아니라면 현재 행의 길이인 result의 두 번쨰 값에 curr을 더해준다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfLinesToWriteString.java){:target="_blank"}에서 확인 가능합니다.