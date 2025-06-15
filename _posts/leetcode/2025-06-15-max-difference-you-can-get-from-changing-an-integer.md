---
title: "Leetcode Java Max Difference You Can Get From Changing an Integer"
excerpt: "Leetcode - 'Max Difference You Can Get From Changing an Integer' 문제 Java 풀이"
last_modified_at: 2025-06-15T11:20:00
header:
  image: /assets/images/leetcode/max-difference-you-can-get-from-changing-an-integer.png
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
[Link](https://leetcode.com/problems/max-difference-you-can-get-from-changing-an-integer/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxDiff(int num) {
    String str = Integer.toString(num);
    char[] charArray = str.toCharArray();
    String max = str;
    String min = str;
    for (char c : charArray) {
      if (c != '9') {
        max = str.replace(c, '9');
        break;
      }
    }
    if (str.charAt(0) != '1') {
      return Integer.parseInt(max) - Integer.parseInt(str.replace(charArray[0], '1'));
    }
    for (int i = 1; i < str.length(); i++) {
      if (charArray[i] != '0' && charArray[i] != '1') {
        min = str.replace(charArray[i], '0');
        break;
      }
    }
    return Integer.parseInt(max) - Integer.parseInt(min);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/max-difference-you-can-get-from-changing-an-integer/submissions/1664324379/){:target="_blank"}

# 설명
1. num을 이용하여 아래 연산을 서로 다른 두 숫자를 선택하여 수행한 최대 차잇값을 반환한다.
- num의 숫자들 중 하나의 숫자를 선택하여 [0, 9] 범위 내 숫자로 바꾼다.
- 바꾼 숫자의 앞은 0이 되면 안된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- str은 num을 문자열로 변환한 변수이다.
- charArray는 str의 문자 배열을 저장한 변수이다.
- max와 min은 수행한 결과의 차이가 최대가 되기 위한 최댓값과 최솟값을 저장할 변수로, 아래의 값으로 초기화한다.
  - max는 str의 앞에서 부터 '9'가 아닌 값을 선택하여 해당 값을 모두 '9'로 바꾼 문자열로 초기화한다.
  - min은 str로 초기화한다.

3. str의 첫 문자가 1이 아닌 경우, max와 str의 첫 문자를 1로 변환한 두 문자열을 숫자로 치환하여 차잇값을 주어진 문제의 결과로 반환한다.

4. 1부터 str의 길이 미만까지 i를 증가시키며 charArray[i] 문자가 '0'과 '1'이 아닌 경우, min에 str 내 해당 문자와 동일한 문자를 '0'으로 변환하여 넣어준다.

5. 위의 수행이 완료되어 저장된 max와 min을 숫자로 변환하여 두 값의 차잇값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaxDifferenceYouCanGetFromChangingAnInteger.java){:target="_blank"}에서 확인 가능합니다.