---
title: "Leetcode Java Maximum Product of Word Lengths"
excerpt: "Leetcode Maximum Product of Word Lengths Java 풀이"
last_modified_at: 2021-12-26T15:00:00
header:
  image: /assets/images/leetcode/maximum-product-of-word-lengths.png
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
[Link](https://leetcode.com/problems/maximum-product-of-word-lengths/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxProduct(String[] words) {
    int length = words.length;
    int[] value = new int[length];
    for (int i = 0; i < length; i++) {
      for (char c : words[i].toCharArray()) {
        value[i] |= 1 << (c - 'a');
      }
    }
    int result = 0;
    for (int i = 0; i < length; i++) {
      int iThWordLength = words[i].length();
      for (int j = i + 1; j < length; j++) {
        if ((value[i] & value[j]) == 0) {
          result = Math.max(result, iThWordLength * words[j].length());
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/607402920/){:target="_blank"}

# 설명
1. 주어진 문자열 배열인 words를 이용하여 중복되지 않은 문자들로 이루어진 두 문자열의 길이 곱이 가장 큰 값을 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 저으이한다.
- length는 words의 길이를 저장하기 위한 변수이다.
- value는 각 문자열의 bit를 저장하기 위한 변수로, 모든 문자열을 이용하여 아래를 통해 값을 넣어준다.
  - value의 i번째 값과 1을 $c - 'a'(97)$ 값만큼 비트를 왼쪽으로 이동시킨 값의 OR(&#124;) 비트 연산의 결과를 value의 i번째에 넣어준다.

3. 결과를 담을 result를 0으로 초기화 하여 선언한다.

4. 0부터 length까지 반복하여 result에 결과를 넣어준다.
- i번째 단어의 길이를 저장할 iThWordLegnth에 words의 i번쨰 문자의 길이를 넣어준다.
- $i + 1$ 부터 length까지 반복하면서 value의 i번째 값과 value의 j번째 값의 AND(&) 비트 연산 결과가 0인 경우, 아래를 수행한다.
  - result에 result와 words의 i번째 문자 길이와 words의 j번쨰 문자 길이의 곱 중 큰 값을 넣어준다.

5. 반복이 완료되면 중복되지 않은 문자들로 이루어진 두 문자열의 길이 곱이 가장 큰 값을 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumProductOfWordLengths.java){:target="_blank"}에서 확인 가능합니다.