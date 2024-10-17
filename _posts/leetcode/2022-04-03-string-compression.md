---
title: "Leetcode Java String Compression"
excerpt: "Leetcode - 'String Compression' 문제 Java 풀이"
last_modified_at: 2022-04-03T09:00:00
header:
  image: /assets/images/leetcode/string-compression.png
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
[Link](https://leetcode.com/problems/string-compression/){:target="_blank"}

# 코드
```java
class Solution {

  public int compress(char[] chars) {
    int i = 0;
    int j = 0;
    int index = 0;
    int length = chars.length;
    while (j < length) {
      int count = 0;
      char curr = chars[i];
      while (j < length && chars[j] == curr) {
        j++;
        count++;
      }
      chars[index++] = curr;
      if (count > 1) {
        if (count < 10) {
          chars[index++] = (char) (count + '0');
        } else {
          for (char c : String.valueOf(count).toCharArray()) {
            chars[index++] = c;
          }
        }
      }
      i = j;
    }
    return index;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/672559481/){:target="_blank"}

# 설명
1. 문자 배열인 chars가 주어지면 아래의 규칙대로 문자 배열을 생성할 때, 길이를 구하는 문제이다.
- 동일한 문자 그룹의 길이가 1개일 경우, 해당 문자만 문자 배열에 넣어준다.
- 2개 이상인 경우, 문자 뒤에 개수를 문자 배열에 넣어준다.
- 문자열의 개수가 10개를 넘어가면, 한 자리씩 잘라서 문자 배열에 넣어준다.
- 주어진 배열을 그대로 사용하여, 새 길이를 구한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- i와 j는 chars를 탐색하여 문자의 개수를 탐색하기 위한 변수로, 둘 다 0으로 초기화한다.
- index는 조건에 만족하는 배열 내 위치를 저장할 변수로, 0으로 초기화한다.
- length는 chars의 길이를 저장할 변수로, chars의 길이로 초기화한다.

3. j가 length 미만일 때 까지 반복하여 아래를 수행한다.
- 문제 풀이에 필요한 변수를 정의한다.
  - count는 동일한 문자의 개수를 계산할 변수로, 0으로 초기화한다.
  - curr은 현재 위치의 문자를 저장할 변수로, chars의 i번째 문자를 넣어준다.
- j가 length 미만이고 char[j]가 curr과 동일할 때 까지 반복하여 j와 count를 증가시켜준다.
- chars의 index번째 위치에 curr을 넣어주고, index를 증가시킨다.
- count가 1 초과이고 count가 10 미만인 경우, chars의 index번째 위치에 count를 ASCII 코드값으로 증가시키고 문자로 변환하여 넣어주고 index를 증가시킨다.
- count가 1 초과이고 count가 10 초과인 경우, count를 문자열로 변환하여 chars의 index번째 위치에 차례대로 넣어주면서 index를 증가시킨다.
- j번째 문자까지 처리하였으므로, i에 j를 넣어 다음 반복의 위치를 j로 지정해준다.

4. 반복이 완료되면 조건을 만족하는 새 문자 배열의 길이인 index를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/StringCompression.java){:target="_blank"}에서 확인 가능합니다.