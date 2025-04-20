---
title: "Leetcode Java Search Suggestions System"
excerpt: "Leetcode - 'Search Suggestions System' 문제 Java 풀이"
last_modified_at: 2025-04-20T15:30:00
header:
  image: /assets/images/leetcode/search-suggestions-system.png
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
[Link](https://leetcode.com/problems/search-suggestions-system/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<String>> suggestedProducts(String[] products, String searchWord) {
    Arrays.sort(products);
    StringBuilder sb = new StringBuilder();
    List<List<String>> result = new ArrayList<>();
    for (char c : searchWord.toCharArray()) {
      sb.append(c);
      String prefix = sb.toString();
      int index = Arrays.binarySearch(products, prefix);
      if (index < 0) {
        index = -index - 1;
      }
      List<String> list = new ArrayList<>();
      for (int j = index; list.size() < 3 && j < products.length && products[j].startsWith(prefix); j++) {
        list.add(products[j]);
      }
      result.add(list);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/search-suggestions-system/submissions/1612230744/){:target="_blank"}

# 설명
1. searchWord의 각 문자를 입력할때마다 제품 목록인 products 내 사전적으로 유사한 상위 3개 제품을 반환하는 문제이다.

2. products의 문자열들을 오름차순 정렬한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- sb는 searchWord를 한 문자씩 입력할 때 현재까지 입력된 문자열을 동적으로 저장할 변수로, StringBuilder로 초기화한다.
- result는 결과 문자열들을 저장할 변수로, ArrayList로 초기화한다.

4. searchWord의 각 문자들을 순차적으로 c에 넣고 아래를 반복한다.
- sb에 c를 이어주고, prefix에 sb의 현재까지 입력된 문자들을 문자열로 변환해서 넣어준다.
- index는 products에서 prefix에 해당하는 문자열의 이진 탐색 위치를 넣어준다.
- index가 0 이하인 음수인 경우, 양수로 변경 후 1울 빼준다.
- list는 현재 검색할 상위 3개 제품을 넣을 변수로, ArrayList로 초기화한다.
- index부터 list의 길이가 3 미만이면서 j가 제품 갯수 미만이고 products[j]의 문자가 prefix로 시작할 때 까지 j를 증가시키며 list에 products[j] 문자열을 넣어준다.
- result에 현재 문자열까지 유사한 제품 목록이 저장된 list를 넣어준다.

5. 반복이 완료되면 각 문자열 목록들이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SearchSuggestionsSystem.java){:target="_blank"}에서 확인 가능합니다.