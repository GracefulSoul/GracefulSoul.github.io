---
title: "Leetcode Java Ransom Note"
excerpt: "Leetcode Ransom Note Java 풀이"
last_modified_at: 2022-02-11T12:00:00
header:
  image: /assets/images/leetcode/ransom-note.png
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
[Link](https://leetcode.com/problems/ransom-note/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canConstruct(String ransomNote, String magazine) {
    int[] count = new int[26];
    for (char ransomNoteChar : ransomNote.toCharArray()) {
      int num = ransomNoteChar - 'a';
      int preIndex = count[num];
      int index = magazine.indexOf(ransomNoteChar, preIndex);
      if (index == -1) {
        return false;
      }
      count[num] = index + 1;
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/638979205/){:target="_blank"}

# 설명
1. 주어진 문자열 magazine이 주어지면 해당 문자들로 ransomNote를 만들 수 있는지 검증하는 문제이다.
- 단, magazine의 문자는 한 번만 사용할 수 있다.

2. count 정수 배열을 영문자의 개수인 26의 크기로 정의한다.

3. ransomNote의 문자들을 반복하여 검증을 수행한다.
- num에 ransomNoteChar에 'a'(26)을 뺀 영문자 순서를 넣어준다.
- preIndex에 count에서 num번째 값인 기존에 위치했던 ransomNoteChar의 위치 값을 넣어준다.
- index에 magazine에서 preIndex 이후의 자리 중 ransomNoteChar의 값을 넣어준다.
- index가 -1인 경우 magazine에 ransomNoteChar가 더 이상 존재하지 않는다는 의미이므로, false를 주어진 문제의 결과로 반환한다.
- count의 num번째 위치에 $index + 1$을 넣어 다음 검색에 그 위치 이후에서 검색할 수 있게하고, 반복을 계속 수행한다.

4. 반복이 완료되면 ransomNote의 문자들이 magazine에 모두 포함되므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RansomNote.java){:target="_blank"}에서 확인 가능합니다.