---
title: "Leetcode Java Groups of Special-Equivalent Strings"
excerpt: "Leetcode - 'Groups of Special-Equivalent Strings' 문제 Java 풀이"
last_modified_at: 2023-04-04T21:40:00
header:
  image: /assets/images/leetcode/groups-of-special-equivalent-strings.png
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
[Link](https://leetcode.com/problems/groups-of-special-equivalent-strings){:target="_blank"}

# 코드
```java
class Solution {

  public int numSpecialEquivGroups(String[] words) {
    Set<String> set = new HashSet<>();
    for (String word : words) {
      int length = word.length();
      char[] even = new char[(length + 1) / 2];
      char[] odd = new char[length / 2];
      for (int i = 0; i < length; i++) {
        if (i % 2 == 0) {
          even[i / 2] = word.charAt(i);
        } else {
          odd[i / 2] = word.charAt(i);
        }
      }
      Arrays.sort(even);
      Arrays.sort(odd);
      set.add(Arrays.toString(odd) + Arrays.toString(even));
    }
    return set.size();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/groups-of-special-equivalent-strings/submissions/927833927/){:target="_blank"}

# 설명
1. 길이가 같은 문자열의 배열인 words를 이용하여 홀수 위치, 혹은 짝수 위치 끼리 문자를 변환하여 동일하게 맞출 수 있는 고유 문자열의 수를 구하는 문제이다.

2. set은 고유 문자열을 저장하기 위한 변수로, 중복을 배제하기 위해 HashSet으로 초기화한다.

3. words의 모든 문자열을 word에 넣어 아래를 반복한다.
- 고유 문자열의 수를 구하기 위한 변수를 정의한다.
  - length는 word의 기링을 저장한 변수이다.
  - even은 짝수 위치의 문자를 저장할 변수로, $\frac{length + 1}{2}$ 크기의 문자 배열로 초기화한다.
  - odd는 홀수 위치의 문자를 저장할 변수로, $\frac{length}{2}$ 크기의 문자 배열로 초기화한다.
- 0부터 length 미만까지 i를 증가시키며 홀수 위치의 문자는 odd에, 짝수 위치의 문자는 even에 순차적으로 넣어준다.
- 문자를 다 넣었으면 even과 odd를 오름차순 정렬 후 odd와 event을 문자열로 변환하여 합친 문자를 set에 넣어준다.

4. 반복이 완료되면 고유 문자열의 갯수가 저장된 set의 크기를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/GroupsOfSpecialEquivalentStrings.java){:target="_blank"}에서 확인 가능합니다.