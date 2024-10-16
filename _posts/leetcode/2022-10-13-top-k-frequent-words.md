---
title: "Leetcode Java Top K Frequent Words"
excerpt: "Leetcode Top K Frequent Words Java"
last_modified_at: 2022-10-13T19:55:00
header:
  image: /assets/images/leetcode/top-k-frequent-words.png
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
[Link](https://leetcode.com/problems/top-k-frequent-words){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> topKFrequent(String[] words, int k) {
    Map<String, Integer> map = new HashMap<>();
    for (String word : words) {
      map.put(word, map.getOrDefault(word, 0) + 1);
    }
    Queue<String> queue = new PriorityQueue<>((String str1, String str2) -> {
      if (map.get(str1) == map.get(str2)) {
        return str1.compareTo(str2);
      } else {
        return map.get(str2) - map.get(str1);
      }
    });
    queue.addAll(map.keySet());
    List<String> result = new ArrayList<>();
    while (k-- > 0) {
      if (!queue.isEmpty()) {
        result.add(queue.poll());
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/821560823/){:target="_blank"}

# 설명
1. words 내 가장 많이 반복된 문자열 k개를 찾아 반환하는 문제이다.
- 반환되는 단어들은 가장 많이 반복된 문자열 순으로, 동일하게 반복된 문자열은 사전 순으로 정렬한다.

2. map은 문자열의 빈도를 저장할 변수로, HashMap으로 초기화하고 words를 반복하여 word 별 발생 횟수를 계산하여 넣어준다.

3. queue는 발생 빈도 순, 사전 순으로 정렬해서 순차적으로 정렬해서 저장할 Queue로, 아래의 규칙대로 정렬하는 PriorityQueue로 초기화한다.
- str1과 str2의 발생 빈도가 같은 경우, 두 단어는 사전순으로 정렬한다.
- str1과 str2의 발생 빈도가 다른 경우, 발생 빈도가 큰 순서로 정렬한다.

4. 3번에서 정의한 queue에 map의 key들을 모두 넣어 queue에 정렬시킨다.

5. result는 결과를 반환할 변수로, ArrayList로 초기화한다.

6. k이 0 이상일 때 까지 아래를 반복하고, k를 감소시킨다.
- queue가 비어있지 않으면, result에 queue의 값을 꺼내 넣어준다.

7. 반복이 완료되면 words 내 가장 많이 반복된 문자열 k개를 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TopKFrequentWords.java){:target="_blank"}에서 확인 가능합니다.