---
title: "Leetcode Java Reverse String II"
excerpt: "Leetcode Reverse String II Java"
last_modified_at: 2022-06-23T19:00:00
header:
  image: /assets/images/leetcode/reverse-string-ii.png
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
[Link](https://leetcode.com/problems/reverse-string-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public String reverseStr(String s, int k) {
    char[] array = s.toCharArray();
    int length = array.length;
    int i = 0;
    while (i < length) {
      int j = Math.min(i + k - 1, length - 1);
      this.swap(array, i, j);
      i += 2 * k;
    }
    return new String(array);
  }

  private void swap(char[] array, int left, int right) {
    while (left < right) {
      char temp = array[left];
      array[left++] = array[right];
      array[right--] = temp;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/729193034/){:target="_blank"}

# 설명
1. s의 매 처음부터 k번째 값과 매 2k번쨰 위치에서 k개의 문자들을 역순으로 반전시켜준다.

2. 문제 풀이에 필요한 변수를 정의한다.
- array는 s를 문자 배열로 변환하여 저장한 배열이다.
- length는 array의 길이를 저장한 변수이다.
- i는 위치를 저장할 변수이다.

3. i가 length 미만까지 아래를 수행한다.
- j에 $i + k - 1$ 혹은 문자의 길이를 벗어날 경우에 마지막 값인 $length - 1$ 중 작은 값을 넣어준다.
- array의 i번째 문자부터 j번째 문자까지 순서를 역순으로 반전시킨다.
- i에 다음 위치인 $2 \times k$의 위치로 이동시켜준다.

4. 반복이 완료되면 array를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReverseStringII.java){:target="_blank"}에서 확인 가능합니다.