---
title: "Leetcode Java Mini Parser"
excerpt: "Leetcode Mini Parser Java 풀이"
last_modified_at: 2022-02-13T17:00:00
header:
  image: /assets/images/leetcode/mini-parser.png
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
[Link](https://leetcode.com/problems/mini-parser/){:target="_blank"}

# 코드
```java
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *     // Constructor initializes an empty nested list.
 *     public NestedInteger();
 *
 *     // Constructor initializes a single integer.
 *     public NestedInteger(int value);
 *
 *     // @return true if this NestedInteger holds a single integer, rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds, if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // Set this NestedInteger to hold a single integer.
 *     public void setInteger(int value);
 *
 *     // Set this NestedInteger to hold a nested list and adds a nested integer to it.
 *     public void add(NestedInteger ni);
 *
 *     // @return the nested list that this NestedInteger holds, if it holds a nested list
 *     // Return empty list if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
class Solution {

  private int start;
  private char[] charArray;

  public NestedInteger deserialize(String s) {
    this.start = 0;
    this.charArray = s.toCharArray();
    return this.recursive();
  }

  private NestedInteger recursive() {
    NestedInteger result = new NestedInteger();
    if (this.charArray[this.start] == '[') {
      this.start++;
      this.dfs(result);
    } else {
      int num = 0;
      int posistion = 1;
      if (charArray[this.start] == '-') {
        posistion = -1;
        this.start++;
      }
      while (this.start < this.charArray.length && this.charArray[this.start] <= '9' && this.charArray[this.start] >= '0') {
        num = (num * 10) + (this.charArray[this.start++] - '0');
      }
      result.setInteger(num * posistion);
    }
    return result;
  }

  private void dfs(NestedInteger parent) {
    while (this.charArray[this.start] != ']') {
      parent.add(this.recursive());
      if (this.charArray[this.start] == ',') {
        this.start++;
      }
    }
    this.start++;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/640405550/){:target="_blank"}

# 설명
1. 주어진 문자열 s를 읽어 NestedInteger로 역직렬화 하는 문제이다.
- 각 요소는 정수이거나 List형태로 구성된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- start는 파싱을 시작하기 위한 위치값을 넣기 위한 변수이다.
- charArray는 주어진 문자열 s를 문자 배열로 저장하여 활용하기 위한 변수이다.

3. start를 0으로 charArray를 주어진 문자열 s의 문자 배열로 전환하여 넣어주고, 4번에 정의한 recursive() 메서드를 수행한 결과를 주어진 문제의 결과로 반환한다.

4. 재귀 호출을 이용하여 정수를 파싱하기 위한 recursive() 메서드를 정의한다.
- result 변수에 새 NestedInteger를 생성한다.
  - 소스에서는 해당 interface를 임시 구현한 SimpleNestedInteger로 사용하였다.
- charArray의 start번째 문자가 대괄호 시작 문자('[')인 경우 start를 증가시키고 5번에서 정의한 dfs(NestedInteger parent) 메서드를 호출한다.
- 위의 경우가 아니면 아래를 수행한다.
  - 정수열을 만들기 위한 변수인 num을 0으로, 음수/양수를 구분하기 위한 변수인 position을 1로 초기화 한다.
  - charArray의 start번째 값이 '-'인 경우, position에 -1을 넣고 start를 증가시킨다.
  - start가 charArray의 길이 미만이고, 0과 9 사이의 숫자일 때 까지 반복하여 num에 정수 값을 넣어준다.
  - 반복이 완료되면 result에 특정 정수 값인 num을 position을 곱해서 넣어준다.
- 위로 초기화된 result를 반환한다.

5. [DFS 알고리즘](https://en.wikipedia.org/wiki/Depth-first_search){:target="_blank"}로 문자열 탐색을 수행하는 dfs(NestedInteger parent) 메서드를 완성한다.
- charArray의 start번째 문자가 대괄호 종료 문자(']')가 아닐 때 까지 반복하여 아래를 수행한다.
  - parent에 4번에서 정의한 recursive() 메서드를 수행한 결과를 내부 List에 넣어준다.
  - charArray의 start번째 문자가 콤마(',')인 경우 무시하고 넘어가기 위해 start를 증가시킨다.
- 반복이 종료되면 다음 위치로 이동하기 위해 start를 증가시킨다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MiniParser.java){:target="_blank"}에서 확인 가능합니다.