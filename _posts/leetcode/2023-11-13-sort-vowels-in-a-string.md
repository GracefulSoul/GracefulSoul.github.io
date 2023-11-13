---
title: "Leetcode Java Sort Vowels in a String"
excerpt: "Leetcode Sort Vowels in a String Java"
last_modified_at: 2023-11-13T20:30:00
header:
  image: /assets/images/leetcode/sort-vowels-in-a-string.png
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
[Link](https://leetcode.com/problems/sort-vowels-in-a-string){:target="_blank"}

# 코드
```java
class Solution {

  public String sortVowels(String s) {
    String vowels = "aeiouAEIOU";
    char[] charArray = s.toCharArray();
    int length = charArray.length;
    char[] vowelArray = new char[length];
    int i = 0;
    for (char c : charArray) {
      if (vowels.indexOf(c) != -1) {
        vowelArray[i++] = c;
      }
    }
    Arrays.sort(vowelArray, 0, i);
    StringBuilder sb = new StringBuilder();
    for (int j = i = 0; i < charArray.length; i++) {
      if (vowels.indexOf(charArray[i]) != -1) {
        sb.append(vowelArray[j++]);
      } else {
        sb.append(charArray[i]);
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sort-vowels-in-a-string/submissions/1097866219/){:target="_blank"}

# 설명
1. 문자열 s 내 자음은 그 자리 그대로 유지하고, 모음만 ASCII 코드의 오름차순으로 정렬하여 위치를 바꾸는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- vowels는 모음을 저장한 변수로, 모음 문자열을 대소문자 모두 포함하여 "aeiouAEIOU"로 초기화한다.
- charArray는 s를 문자 배열로 변환하여 저장한 변수이다.
- vowelArray는 모음 문자만 모아서 저장할 변수로, 최대 가능한 문자 갯수인 length 길이의 문자 배열로 초기화한다.
- i는 vowelArray의 처음부터 모음 문자를 넣기 위한 위치 변수로, 0으로 초기화하고 charArray의 모든 문자들을 순차적으로 탐색하여 vowelArray에 넣어준 후 넣은 값들을 오름차순 정렬시켜준다.
- sb는 결과 문자열을 동적으로 생성할 변수로, StringBuilder로 초기화한다.

3. i를 0으로 초기화하고, j를 0으로 정의한 후 charArray의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- charArray[i]의 문자가 모음인 경우, sb에 vowelArray[j]의 문자를 넣어주고 j를 증가시킨다.
- 위의 경우가 아니라면, sb에 charArray[i]의 문자를 넣어준다.

4. 반복이 완료되면 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SortVowelsInAString.java){:target="_blank"}에서 확인 가능합니다.