---
title: "Leetcode Java Find Smallest Letter Greater Than Target"
excerpt: "Leetcode - 'Find Smallest Letter Greater Than Target' 문제 Java 풀이"
last_modified_at: 2022-12-01T12:50:00
header:
  image: /assets/images/leetcode/find-smallest-letter-greater-than-target.png
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
[Link](https://leetcode.com/problems/find-smallest-letter-greater-than-target){:target="_blank"}

# 코드
```java
class Solution {

  public char nextGreatestLetter(char[] letters, char target) {
    int length = letters.length;
    int left = 0;
    int right = length;
    while (left < right) {
      int mid = left + ((right - left) / 2);
      if (letters[mid] > target) {
        right = mid;
      } else {
        left = mid + 1;
      }
    }
    return letters[left % length];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/852627234/){:target="_blank"}

# 설명
1. 사전적 순서가 증가하는 형태의 문자 배열인 letters 이용하여 target 다음으로 큰 문자를 찾는 문제이다.
- 단, 해당 문자가 존재하지 않은 경우 letters의 첫 문자를 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 letters의 길이를 저장한 변수이다.
- left와 right는 문자열 탐색의 기준이 될 위치 값으로, 0과 length로 초기화한다.

3. left가 right보다 작을 때 까지 아래를 반복하여 문자를 탐색한다.
- mid에 중앙값인 $left + \frac{right - left}{2}$를 넣어준다.
- letters의 mid번째 문자가 target보다 크면 right에 mid를, 그렇지 않으면 left에 $mid + 1$을 넣어 탐색을 계속한다.

4. letters 내 left를 length로 나눈 나머지 값의 위치에 해당하는 문자를 주어진 문제의 결과로 반환한다.
- 모든 문자 탐색하여 해당 문자를 찾지 못한 경우 left와 length는 동일하므로, 나눈 결과의 나머지인 0번째 문자를 반환하기 위함이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindSmallestLetterGreaterThanTarget.java){:target="_blank"}에서 확인 가능합니다.