---
title: "Leetcode Java Palindrome Partitioning"
excerpt: "Leetcode - 'Palindrome Partitioning' 문제 Java 풀이"
last_modified_at: 2021-08-20T12:00:00
header:
  image: /assets/images/leetcode/palindrome-partitioning.png
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
[Link](https://leetcode.com/problems/palindrome-partitioning/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<String>> partition(String s) {
    List<List<String>> result = new ArrayList<>();
    this.recursive(s, 0, result, new ArrayList<>());
    return result;
  }

  private void recursive(String s, int index, List<List<String>> result, List<String> temp) {
    if (index == s.length()) {
      result.add(new ArrayList<>(temp));
    } else {
      for (int i = index; i < s.length(); i++) {
        if (this.isPalindrome(s, index, i)) {
          temp.add(s.substring(index, i + 1));
          this.recursive(s, i + 1, result, temp);
          temp.remove(temp.size() - 1);
        }
      }
    }
  }

  private boolean isPalindrome(String s, int start, int end) {
    while (start < end) {
      if (s.charAt(start++) != s.charAt(end--)) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/541182257/){:target="_blank"}

# 설명
1. 주어진 문자열 s를 이용하여 앞뒤로 읽어도 같은 문자열(이하 회문)을 모두 찾는 문제이다.

2. 재귀 호출을 이용하여 List인 result에 회문의 조합을 확인하여 넣어준다.

3. index가 s.length()와 동일한 경우 마지막 문자열까지 탐색한 경우이므로, result에 회문을 저장한 temp를 새 객체로 생성하여 넣어준다.

4. 그 외의 경우 index부터 s.length()까지 반복하여 문자열 s의 index부터 i까지의 부분 문자열이 회문인 경우 아래를 수행한다.
- 반복을 통한 회문을 저장하는 변수 temp에 해당 문자열을 넣어준다.
- index를 $i + 1$로 변경하고 재귀 호출을 수행하여 문자열 s의 회문을 탐색한다.
- 위의 재귀 호출이 완료되면 해당 문자열 중 마지막 입력된 문자열을 제거하고 다시 반복문을 수행한다.

5. 재귀 호출이 완료되면 주어진 문자열 s의 회문 조합을 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PalindromePartitioning.java){:target="_blank"}에서 확인 가능합니다.