---
title: "Leetcode Java Sort Characters By Frequency"
excerpt: "Leetcode Sort Characters By Frequency Java 풀이"
last_modified_at: 2022-04-10T14:00:00
header:
  image: /assets/images/leetcode/sort-characters-by-frequency.png
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
[Link](https://leetcode.com/problems/sort-characters-by-frequency/){:target="_blank"}

# 코드
```java
class Solution {

  public String frequencySort(String s) {
    int[][] count = new int[128][2];
    for (char c : s.toCharArray()) {
      count[c][0] = c;
      count[c][1]++;
    }
    Arrays.sort(count, (a, b) -> (b[1] - a[1]));
    StringBuilder sb = new StringBuilder();
    for (int idx = 0; idx < count.length; idx++) {
      while (count[idx][1] > 0) {
        sb.append((char) count[idx][0]);
        count[idx][1]--;
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/677421302/){:target="_blank"}

# 설명
1. 문자열 s에서 가장 많이 존재하는 문자의 내림차순으로 재 배열한 결과를 반환하는 문제이다.

2. 문자열의 발생 빈도를 계산하기 위한 count 배열을 정의하고, 2차원 정수 배열의 [128][2] 크기로 초기화한다.
- 문자열은 영어 대소문자, 숫자로 구성되어 배열의 행 크기를 ASCII 코드의 최대 크기인 128 크기로 정의한다.
- 문자의 발생 빈도로 정렬을 수행해야 하므로 문자와 빈도를 저장하기 위해서 배열의 열 크기를 2로 정의한다.

3. 문자열 s를 반복하여 count에 문자와 발생 빈도를 넣어주고, 발생 빈도를 이용하여 내림차순 정렬을 수행한다.

4. 내림차순으로 정렬된 문자열을 생성하기 위해 sb를 StringBuilder로 정의한다.
- 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.

5. 0부터 count의 길이까지 idx를 증가시키며 반복하여 아래를 수행한다.
- count[idx][1]인 발생 빈도가 0 초과인 경우, sb에 count[idx][0] 값인 발생 문자의 ASCII Code 값을 문자로 변환하여 넣어주고 count[idx][1]인 발생 빈도를 감소시켜준다.

6. 반복이 완료되면 발생 빈도를 내림차순으로 정렬해서 넣은 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SortCharactersByFrequency.java){:target="_blank"}에서 확인 가능합니다.