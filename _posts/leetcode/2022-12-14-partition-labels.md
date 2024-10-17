---
title: "Leetcode Java Partition Labels"
excerpt: "Leetcode - 'Partition Labels' 문제 Java 풀이"
last_modified_at: 2022-12-14T05:10:00
header:
  image: /assets/images/leetcode/partition-labels.png
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
[Link](https://leetcode.com/problems/partition-labels){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> partitionLabels(String s) {
    char[] charArray = s.toCharArray();
    int length = charArray.length;
    int[] last = new int[26];
    for (int idx = 0; idx < length; idx++) {
      last[charArray[idx] - 'a'] = idx;
    }
    List<Integer> result = new ArrayList<>();
    int start = 0;
    int end = 0;
    for (int idx = 0; idx < length; idx++) {
      int index = last[charArray[idx] - 'a'];
      if (index > end) {
        end = index;
      }
      if (end == idx) {
        result.add(end - start + 1);
        start = end + 1;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/partition-labels/submissions/859347905/){:target="_blank"}

# 설명
1. s의 문자열을 최대한 같은 문자열끼리 묶어 가능한 많은 부분 문자열로 분리할 때, 각 문자열의 길이를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s를 문자 배열로 변환하여 저장하는 변수이다.
- length는 charArray의 길이를 저장하는 변수이다.
- last는 charArray의 각 문자 별 마지막 위치를 담기 위한 변수로, 알파벳 개수인 26 크기로 정의하고 charArray를 반복하여 last에 각 문자 별 마지막 위치를 넣어준다.
- result는 분리한 문자열의 길이를 저장할 변수로, ArrayList로 초기화한다.
- start와 end는 각 부분 문자열을 분리하기 위해 사용될 위치 변수로, 모두 0으로 초기화한다.

3. 0부터 length까지 idx를 증가시키며 아래를 수행한다.
- index에 charArray의 idx번째 문자의 마지막 위치 값을 last에서 찾아 넣어준다.
- index가 end보다 큰 경우, end에 index를 넣어 종료 위치를 갱신시켜준다.
- end와 idx가 동일하면 해당 위치까지 부분 문자열로 자를 수 있으므로 아래를 수행한다.
  - result에 $end - start + 1$인 부분 문자열의 길이를 넣어준다.
  - start에 $end + 1$인 다음 문자 위치를 넣어 다음 부분 문자열 계산을 준비한다.

4. 반복이 완료되면 부분 문자열의 길이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PartitionLabels.java){:target="_blank"}에서 확인 가능합니다.