---
title: "Leetcode Java Iterator for Combination"
excerpt: "Leetcode - 'Iterator for Combination' 문제 Java 풀이"
last_modified_at: 2025-08-15T10:20:00
header:
  image: /assets/images/leetcode/iterator-for-combination.png
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
[Link](https://leetcode.com/problems/iterator-for-combination/){:target="_blank"}

# 코드
```java
class CombinationIterator {

  private List<String> list;
  private int index;

  public CombinationIterator(String characters, int combinationLength) {
    this.list = new ArrayList<>();
    this.index = 0;
    this.dfs(characters.toCharArray(), combinationLength, 0, new StringBuilder());
  }

  public String next() {
    return this.list.get(this.index++);
  }

  public boolean hasNext() {
    return this.index < this.list.size();
  }

  private void dfs(char[] characters, int combinationLength, int start, StringBuilder sb) {
    if (combinationLength == 0) {
      this.list.add(sb.toString());
    } else {
      for (int i = start; i <= characters.length - combinationLength; i++) {
        sb.append(characters[i]);
        this.dfs(characters, combinationLength - 1, i + 1, sb);
        sb.deleteCharAt(sb.length() - 1);
      }
    }
  }

}

/**
 * Your CombinationIterator object will be instantiated and called as such:
 * CombinationIterator obj = new CombinationIterator(characters, combinationLength);
 * String param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
```

# 결과
[Link](https://leetcode.com/problems/iterator-for-combination/submissions/1735502042/){:target="_blank"}

# 설명
1. 아래 기능을 수행하는 CombinationIterator 객체를 설계하는 문제이다.
- 생성자인 CombinationIterator(string characters, int combinationLength)는 정렬된 서로 다른 영소문자로 구성된 characters와 조합 문자열의 길이인 combinationLength로 객체를 초기화한다.
- 메서드인 next()는 combinationLength 길이의 사전적 다음 순서의 문자열 조합을 반환한다.
- 메서드인 hasNext()는 다음 조합 문자가 존재하는지 여부를 반환한다.

2. 객체의 조합 문자열 구성에 필요한 전역 변수를 정의한다.
- list는 조합 문자열을 구성하여 저장할 변수이다.
- index는 조합 문자열이 저장된 위치 변수이다.

3. 조합 문자열 생성에 필요한 dfs(char[] characters, int combinationLength, int start, StringBuilder sb) 메서드를 정의한다.
- combinationLength가 0인 경우, list에 sb를 문자열로 변환하여 넣어준다.
- combinationLength가 0이 아닌 경우, start부터 characters의 길이에서 combinationLength 값을 뺀 값 이하까지 i를 증가시키며 아래를 반복한다.
  - sb에 characters의 i번째 문자를 넣어준다.
  - combinationLength를 1 감소시키고, start를 1 증가시켜 재귀 호출을 수행한다.
  - sb에서 마지막 문자를 제거해준다.

4. 생성자인 CombinationIterator(string characters, int combinationLength)를 구성한다.
- 전역 변수인 list를 ArrayList로, index를 0으로 초기화한다.
- 3번에서 정의한 dfs(char[] characters, int combinationLength, int start, StringBuilder sb) 메서드를 characters를 문자 배열로, start를 0으로, sb에 새 StringBuilder로 초기화하여 수행하여 combinationLength 길이의 조합 문자열을 list에 모두 넣어 객체를 초기화한다.

5. 메서드인 next()를 구성한다.
- list의 index번째 문자열인 바로 다음 조합 문자열을 반환 후 index를 증가시켜준다.

6. 메서드인 hasNext()를 구성한다.
- index가 list의 길이 미만인 마지막 위치가 아닌지 여부를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/IteratorForCombination.java){:target="_blank"}에서 확인 가능합니다.